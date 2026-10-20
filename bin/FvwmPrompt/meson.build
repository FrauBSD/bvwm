# Fvwmprompt is written in golang. Unfortunately there is still
# no automagic in meson to handle golang projects. So we have to
# do it manually.

# Extract all of the go sources from the current directory
r = run_command('find-go-sources.sh', meson.current_source_dir(), check: true)
fvwmprompt_files = r.stdout().strip().split()
fvwmprompt_files += 'go.mod'
fvwmprompt_files += 'go.sum'

fvwmprompt_build = meson.current_source_dir()
fvwmprompt_output = meson.current_build_dir() + '/bvwm-FvwmPrompt'

# Packagers may set GO_CMD and GO_BUILDFLAGS. The flags are written to a
# script so quoted -ldflags stay shell syntax, and so -C stays the first
# go build flag. Unset, the command below is go build -mod=vendor.
go_wrapper = meson.current_build_dir() / 'bvwm-go-build'
run_command(
    'sh', '-c',
    '''
out=$1
rm -f "$out"
if [ -z "$GO_CMD" ]; then
    exit 0
fi
cat > "$out" << EOF
#!/bin/sh
exec $GO_CMD build "\$@" $GO_BUILDFLAGS
EOF
chmod 755 "$out"
''',
    'sh', go_wrapper,
    check: true,
)

fvwmprompt = custom_target(
    'bvwm-FvwmPrompt',
    output: 'bvwm-FvwmPrompt',
    input: fvwmprompt_files,
    command: [
        find_program('sh'),
        '-c',
        'w=$1; shift; if [ -x "$w" ]; then shift; exec "$w" "$@"; fi; cmd=$1; shift; exec "$cmd" build "$@"',
        'sh',
        go_wrapper,
        golang.full_path(),
        '-C', fvwmprompt_build,
        '-v',
        '-mod=vendor',
        '-o', fvwmprompt_output,
    ],
    install: true,
    install_dir: bindir,
)

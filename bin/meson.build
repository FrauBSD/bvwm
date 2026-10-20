if golang.found()
    subdir('FvwmPrompt')
endif

# BVWM: prefix PATH helpers so bin/ coinstalls with stock fvwm3.
FvwmCommand = configure_file(
    input: 'FvwmCommand.in',
    output: 'bvwm-FvwmCommand',
    configuration: file_config,
    install: true,
    install_dir: bindir,
    install_mode: install_mask_755,
)

# We should tighten up the dependencies here, but for now we'll just use all_found_deps.
fvwm_root = executable(
    'bvwm-root',
    'fvwm-root.c',
    include_directories: includedirs,
    link_with: libfvwm3,
    dependencies: all_found_deps,
    install: true,
)

fvwm_perllib = configure_file(
    input: 'fvwm-perllib.in',
    output: 'bvwm-perllib',
    configuration: file_config,
    install: true,
    install_dir: bindir,
    install_mode: install_mask_755,
)

fvwm_convert = configure_file(
    input: 'fvwm-convert-2.6.in',
    output: 'bvwm-convert-2.6',
    configuration: file_config,
    install: true,
    install_dir: bindir,
    install_mode: install_mask_755,
)

fvwm_menu_xlock = configure_file(
    input: 'fvwm-menu-xlock.in',
    output: 'bvwm-menu-xlock',
    configuration: file_config,
    install: true,
    install_dir: bindir,
    install_mode: install_mask_755,
)

fvwm_menu_directory = configure_file(
    input: 'fvwm-menu-directory.in',
    output: 'bvwm-menu-directory',
    configuration: file_config,
    install: true,
    install_dir: bindir,
    install_mode: install_mask_755,
)

fvwm_menu_desktop = configure_file(
    input: 'fvwm-menu-desktop.in',
    output: 'bvwm-menu-desktop',
    configuration: file_config,
    install: true,
    install_dir: bindir,
    install_mode: install_mask_755,
)

config_data = install_data(
    'fvwm-menu-desktop-config.fpl',
    install_dir: fvwm_datadir,
)

fvwm_tile = install_data(
    'fvwm-tile',
    install_dir: bindir,
    install_mode: install_mask_755,
)

bvwm_same_class = install_data(
    'bvwm-same-class',
    install_dir: bindir,
    install_mode: install_mask_755,
)

bvwm_super_menu_handler = install_data(
    'bvwm-super-menu-handler',
    install_dir: bindir,
    install_mode: install_mask_755,
)

super_menu_arm = install_data(
    'super-menu-arm',
    install_dir: bindir,
    install_mode: install_mask_755,
)

super_menu_release = install_data(
    'super-menu-release',
    install_dir: bindir,
    install_mode: install_mask_755,
)

super_menu_open = install_data(
    'super-menu-open',
    install_dir: bindir,
    install_mode: install_mask_755,
)

bhotkeys_bvwm_run = install_data(
    'bhotkeys-bvwm-run',
    install_dir: bindir,
    install_mode: install_mask_755,
)

install_data(
    [
        '../share/bhotkeys/plugins.d/bvwm-focus-back',
        '../share/bhotkeys/plugins.d/bvwm-focus-class',
        '../share/bhotkeys/plugins.d/bvwm-focus-class-back',
        '../share/bhotkeys/plugins.d/bvwm-focus-next',
        '../share/bhotkeys/plugins.d/bvwm-tile-auto',
        '../share/bhotkeys/plugins.d/bvwm-tile-bottom',
        '../share/bhotkeys/plugins.d/bvwm-tile-bottom-left',
        '../share/bhotkeys/plugins.d/bvwm-tile-bottom-right',
        '../share/bhotkeys/plugins.d/bvwm-tile-down',
        '../share/bhotkeys/plugins.d/bvwm-tile-insert',
        '../share/bhotkeys/plugins.d/bvwm-tile-left',
        '../share/bhotkeys/plugins.d/bvwm-tile-right',
        '../share/bhotkeys/plugins.d/bvwm-tile-rotate',
        '../share/bhotkeys/plugins.d/bvwm-tile-top',
        '../share/bhotkeys/plugins.d/bvwm-tile-top-left',
        '../share/bhotkeys/plugins.d/bvwm-tile-top-right',
        '../share/bhotkeys/plugins.d/bvwm-tile-up',
    ],
    install_dir: join_paths(get_option('datadir'), 'bhotkeys', 'plugins.d'),
)

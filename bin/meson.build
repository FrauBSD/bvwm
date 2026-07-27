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

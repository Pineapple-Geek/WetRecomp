# Switch settings

The app loads `hardware.toml` and `mapping.toml` from this directory. Command-line flags and `REX_*` environment variables override file values.

`hardware.toml` contains the WET-specific options:

- `wet_fps60_unlock`: unlock the frame-rate cap.
- `wet_disable_motion_blur`, `wet_disable_depth_of_field`, `wet_disable_shaky_camera`: disable visual effects.
- `wet_gpu_wait_mode`: `0` spins, `1` yields, and `2` sleeps briefly while waiting for the GPU.
- `user_language`: `1` English, `3` German, `4` French, `5` Spanish, or `6` Italian.

`mapping.toml` selects the native Switch input driver.

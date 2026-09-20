# rofi-vm

Personal Rofi launcher for libvirt virtual machines. It discovers domain XML
files, starts the selected VM with `virsh`, tries Looking Glass first, and falls
back to an RDP connection.

## Build and install

```bash
nix build github:RevolunixOS/pkg-rofi-vm
nix profile install github:RevolunixOS/pkg-rofi-vm
```

## Configuration

The script sources `~/.config/rdp-id.sh` and expects:

```bash
MDP="your-rdp-password"
SCALE="100"
```

Do not commit that file. Restrict its permissions because the password is read
as shell code and passed to FreeRDP on the command line.

## Usage

```bash
rofi-vm
```

## Host assumptions

- libvirt domain XML files are read from `/var/lib/libvirt/qemu`;
- the invoking user can run `sudo virsh start`;
- `looking-glass-client` is installed separately;
- RDP is reachable at the fixed address `192.168.122.254`;
- the RDP username matches the local `$USER`;
- the Rofi theme selector exists at
  `~/.config/rofi/applets/shared/theme.bash`.

The wrapper provides Rofi and FreeRDP but does not provide `virsh` or Looking
Glass. Adapt the paths, address, authentication handling, and package
dependencies before general use.

## License

See [`LICENSE`](LICENSE).

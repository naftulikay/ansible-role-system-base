# ansible-role-system-base [![Build Status][img-build-status]][build-status]

Provides common base system configuration.

This role is primarily useful on macOS because of its invalid claims of being Unix, and requires a lot of
normalization for it to be useful.

Available on Ansible Galaxy at [`naftulikay.system-base`][galaxy].

## Requirements

Supporting (under test) Ubuntu 16.04, elementary OS Loki, CentOS, and macOS. Only amd64 architecture is supported
for now. Other Unix-like environments may work but are not under test.

## Role Variables

<dl>
  <dt><code>macos_user</code></dt>
  <dd>The user for using Homebrew, as Homebrew, in their words, should not be run as root.</dd>
</dl>

## Dependencies

 - [naftulikay.base][naftulikay.base] - Base system facts.

## License

Licensed at your discretion under either:

 - [MIT License](./LICENSE-MIT)
 - [Apache License, Version 2.0](./LICENSE-APACHE)

 [build-status]: https://travis-ci.org/naftulikay/ansible-role-system-base
 [img-build-status]: https://travis-ci.org/naftulikay/ansible-role-system-base.svg?branch=master
 [galaxy]: https://galaxy.ansible.com/naftulikay/system-base/

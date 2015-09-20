rust-xdg
========

rust-xdg is a library that makes it easy to follow the X Desktop Group
standards for data, configuration, cache and runtime directories.

See also [documentation](https://whitequark.github.io/rust-xdg/xdg/).

Installation
------------

Add the following to `Cargo.toml`:

```toml
[dependencies]
xdg = "*"
```

Examples
--------

To store configuration:

```rust
extern crate xdg;
let xdg_dirs = xdg::XdgDirs::new();

let config_path = xdg_dirs.place_config_file("myapp/config.ini");
let mut config_file = try!(File::create(config_path));
try!(write!(&mut config_file, "configured = 1"));
```

The `myapp.ini` file will appear in the proper location for desktop
configuration files, most likely `~/.config/myapp/config.ini`.
The leading directories will be automatically created.

To retrieve supplementary data:

```rust
let logo_path = xdg_dirs.find_config_file("myapp/logo.png")
                          .expect("application data not present");
let mut logo_file = try!(File::open(logo_path));
let mut logo = Vec::new();
try!(logo_file.read_to_end(&mut logo));
```

The `logo.png` will be searched in the proper locations for
supplementary data files, most likely `~/.local/share/myapp/logo.png`,
then `/usr/local/share/myapp/logo.png` and `/usr/share/myapp/logo.png`.

License
-------

rust-xdg is distributed under the terms of both the MIT license
and the Apache License (Version 2.0).

See LICENSE-APACHE and LICENSE-MIT for details.

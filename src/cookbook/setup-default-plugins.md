# Configuring Default Plugins

Using the default plugins is a quick way to create and setup a window, initialise the graphics adapter and be up and running quickly.

These can be configured by using resources, initialising them before including the plugin, like so:

```rust
use bevy::prelude::*;

fn main() {
  App::build()
    .insert_resource(WindowDescriptor {
      // config changes
      ..Default::default()
    })
    .add_plugins(DefaultPlugins)
    .run();
}
```

## Window Descriptor

For the initial window created by the `bevy_window::WindowPlugin`, a resource of type `bevy_window::WindowDescriptor` can be provided. The full type is defined as:

```rust,no_run,noplayground
pub struct WindowDescriptor {
    pub width: f32,
    pub height: f32,
    pub resize_constraints: WindowResizeConstraints,
    pub scale_factor_override: Option<f64>,
    pub title: String,
    pub vsync: bool,
    pub resizable: bool,
    pub decorations: bool,
    pub cursor_visible: bool,
    pub cursor_locked: bool,
    pub mode: WindowMode,
    #[cfg(target_arch = "wasm32")]
    pub canvas: Option<String>,
}
```

You can quickly change a few of these and leave the others on default.

```rust,no_run,noplayground
use bevy::{prelude::*, window::WindowMode};

fn main() {
  App::build()
    .insert_resource(WindowDescriptor {
      title: "The best game ever!".to_owned(),
      width: 1920.0,
      height: 1080.0,
      mode: WindowMode::Windowed,
      ..Default::default()
    })
    .add_plugins(DefaultPlugins)
    .run();
}
```

## Render settings

`bevy_render::RenderPlugin` uses a few resources, only two of which are interesting for initial configuration.

```rust,no_run,noplayground
use bevy::prelude::*;

fn main() {
  App::build()
    .insert_resource(ClearColor(Color::rgb(0.7, 0.7, 1.0)))
    .insert_resource(Msaa { samples: 4 })
    .add_plugins(DefaultPlugins)
    .run();
}
```

To find more of the resources, [this source file](https://github.com/bevyengine/bevy/blob/main/crates/bevy_render/src/lib.rs#L170) is a good starting point.
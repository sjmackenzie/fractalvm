Component Naming and Organization guideline.
---------------------------------------------------------------

A component is a Rust implementation of a flow-based programming component. It has a file extension ending with `*.rs`.
A composite component is programmed in a Flow-base programming language that resembles a graph, It has a file extension ending with `*.fcl`. They reference other components and/or composite components, these components shall be named supporting components.

Components should be placed somewhere in the `components/` tree, i.e. in `components/category/subcategory/.../componentname/`.

A composite component (`*.fcl` file ext) consist of many components (`*.rs` files) and/or composite components. Composite components should have their own folder named after the composite component iff the composite component has specialized components to enable the purpose of the composite component. The entry level component should be called component.fcl.

Normal components (`*.rs` file ext) do not need their own folder name.

For example: a composite component XOR in this example has supporting components, they should be stored in `/development/binary/XOR` folder. In this inefficient implementation of XOR, XOR has the Rust AND, NOT, OR gate components as supporting components in the same folder.

Fractalvm will understand that XOR is a folder and will look for a `component.fcl` in that folder.
```
├── components
│   └── development
│       └── binary
│           └── XOR
│               ├── AND.rs
│               ├── component.fcl
│               ├── NOT.rs
│               └── OR.rs
```
If on the other hand you decided (rightfully so!) to properly categorize your components and make them available to the rest of the community then the below structure is better. In this example the NOT makes use of NAND, AND makes use of NOT and NAND and XOR makes use of AND, NOT and OR. As these `*.fcl` files reference other `*.fcl` + `NAND.rs` it is acceptable for `XOR.fcl` to not have a folder associated with it.
```
├── components
│   └── development
│       └── binary
│           ├── AND.fcl
│           ├── NAND.rs
│           ├── NOT.fcl
│           ├── OR.fcl
│           └── XOR.fcl
```
If for example the XOR has supporting `*.rs` components (which it doesn't) then they would go in the `/components/development/binary/XOR/{composite_component_folder_name, component_name.rs}`.
```
├── components
│   └── development
│       └── binary
│           ├── AND.fcl
│           ├── NAND.rs
│           ├── NOT.fcl
│           ├── OR.fcl
│           └── XOR
│               └── example_supporting_composite_component
│                   └── supporting_component.rs
│                   └── component.fcl
│               └── example_supporting_component.rs
│               └── component.fcl
```
Below are some rules for picking the right category for a set of components. Many components fall under several categories; what matters is the primary purpose of a component. For example the XOR gate goes under `components/development/binary` and not in a cryptography composite component's folder.

Please ensure you correctly place you files and ensure you develop them in a manner which is reusable as possible. These components and composite components can be seen as a toolbox which will grow with you over time.

When in doubt, consider refactoring the components/ tree, e.g. creating new categories or splitting up an existing category.

All examples are taken from the linux world for demonstration purposes only.

Component hierarchy and folder structure:
```
If it’s used to support software development:

	If it’s a library used by other packages:
	development/libraries (e.g. libxml2)

	If it’s a compiler:
	development/compilers (e.g. gcc)

	If it’s an interpreter:
	development/interpreters (e.g. guile)

	If it’s a (set of) development tool(s):
		If it’s a parser generator (including lexers):
		development/tools/parsing (e.g. bison, flex)

		If it’s a build manager:
		development/tools/build-managers (e.g. gnumake)

		Else:
		development/tools/misc (e.g. binutils)

	Else:
	development/misc

If it’s a (set of) tool(s):
(A tool is a relatively small program, especially one intented to be used non-interactively.)

	If it’s for networking:
	tools/networking (e.g. wget)

	If it’s for text processing:
	tools/text (e.g. diffutils)

	If it’s a system utility, i.e., something related or essential to the operation of a system:
	tools/system (e.g. cron)

	If it’s an archiver (which may include a compression function):
	tools/archivers (e.g. zip, tar)

	If it’s a compression program:
	tools/compression (e.g. gzip, bzip2)

	If it’s a security-related program:
	tools/security (e.g. nmap, gnupg)

	Else:
	tools/misc

If it’s a shell:
shells (e.g. bash)

If it’s a server:
	If it’s a web server:
	servers/http (e.g. apache-httpd)

	If it’s an implementation of the X Windowing System:
	servers/x11 (e.g. xorg — this includes the client libraries and programs)

	Else:
	servers/misc

If it’s a desktop environment:
desktops (e.g. kde, gnome, enlightenment)

If it’s a window manager:
applications/window-managers (e.g. awesome, compiz, stumpwm)

If it’s an application:
A (typically large) program with a distinct user interface, primarily used interactively.

	If it’s a version management system:
	applications/version-management (e.g. subversion)

	If it’s for video playback / editing:
	applications/video (e.g. vlc)

	If it’s for graphics viewing / editing:
	applications/graphics (e.g. gimp)

	If it’s for networking:
		If it’s a mailreader:
		applications/networking/mailreaders (e.g. thunderbird)

		If it’s a newsreader:
		applications/networking/newsreaders (e.g. pan)

		If it’s a web browser:
		applications/networking/browsers (e.g. firefox)

		Else:
		applications/networking/misc

	Else:
	applications/misc

If it’s data (i.e., does not have a straight-forward executable semantics):
	If it’s a font:
	data/fonts

	If it’s related to SGML/XML processing:
		If it’s an XML DTD:
		data/sgml+xml/schemas/xml-dtd (e.g. docbook)

If it’s a game:
games

Else:
misc

note: the above is adapted from the nixos file naming and organization guideline

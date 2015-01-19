LitJSON
=======

A *.Net* library to handle conversions from and to JSON (JavaScript Object
Notation) strings.

## Feature log

#### UnityEngine types

Further adaptions allow to pass UnityEngine types directly to the mapper:
```csharp
JsonMapper.ToJson( Vector2.zero ); // Output { "x" : 0, "y" : 0 }
JsonMapper.ToJson( Vector3.one );  // Output { "x" : 1, "y" : 1, "z" : 1 }
```
Of course reading back in also works:
```csharp
var v2 = JsonMapper.ToObject<Vector2>( "{\"x\":0,\"y\":0}" ); 
var v3 = JsonMapper.ToObject<Vector3>( "{\"x\":0,\"y\":0,\"z\":1}" ); 
```

#### float (Single) and long (Int64) types

This fork includes [this patch](https://github.com/SONIC3D/litjson/commit/3cd16e3650f5f03765704b27700d4c3d37781a01.patch) for serializing float(Single) and long(Int64) types from this [pull request](https://github.com/lbv/litjson/pull/25) .




------------

Original README
===============

## Compiling

See the files under the `build` directory.

### Using GNU Make

Change directory to `build/make/` and run `make` from it. This tries to use
the `gmcs` compiler by default. Feel free to open the `Makefile` and tweak
it according to your needs.

### Using other tools

Currently, LitJSON doesn't have any other auxiliary files for compiling this
library with other tools.

If you want to contribute your own solutions to compile it with tools like
*NAnt* or *MSBuild*, that would be most appreciated. Please create those
auxiliary files under the path `build/some-tool`. Thanks.

## Tests

This library comes with a set of unit tests using the [NUnit][nunit]
framework.

If you have [pkg-config][pkg-config] in your system, and the *Mono* suite
provides the `mono-nunit.pc` file, you can try running these tests by running
`make test` from the `build/make` directory.

You can specify which `pkg-config` is invoked by passing a `PKG_CONFIG`
variable to `make test`. This is useful when you have mutiple conflicting
`pkg-config`s on your system and need to select the correct one (i.e. to
avoid conflicts with Homebrew on Mac OSX).

Example of running the tests on Mac OSX:

```bash
# In litjson/ directory
$ cd build/make
$ make PKG_CONFIG=/Library/Frameworks/Mono.framework/Commands/pkg-config test
```

## Using LitJSON from an application

Reference the `LitJson.dll` file when compiling your code. For a link to
download this file, see the *Download* section in the project's
[website][litjson].

Alternatively, just copy the whole tree of files under `src/LitJSON` to your
own project's source tree and integrate it with your development environment.

## License

[Unlicense][unlicense] (public domain).


[litjson]: http://lbv.github.io/litjson/
[nunit]: http://www.nunit.org/
[pkg-config]: http://www.freedesktop.org/wiki/Software/pkg-config
[unlicense]: http://unlicense.org/

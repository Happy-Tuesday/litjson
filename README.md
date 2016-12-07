LitJSON
=======

A *.Net* library to handle conversions from and to JSON (JavaScript Object
Notation) strings flavoured for the Unity3D engine.


## Feature log

#### Attributes

Introducing attributes for JsonMappers when serializing to JSON String Objects. Currently only the ```Ignore``` Attribute is available but future implementations may bring new ones.

```csharp
public class Foo
{
  public string id;
  [LitJson.Ignore]
  public string privateName;
}
```

```LitJson.JsonMapper.ToJson(foo);``` would simply ignore the ```privateMember``` field and only output ```{ "id" : "bar" }```.  
The Attribute is applyable to Classes, Properties and Fields.

#### UnityEngine types

These already work out of the box

```csharp
JsonMapper.ToJson( AnimationCurve.EaseInOut(0,0,1,1) );
```

Further adaptions allow to pass UnityEngine types directly to the mapper:

```csharp
JsonMapper.ToJson( Vector2.zero );         // Output { "x" : 0, "y" : 0 }
JsonMapper.ToJson( Vector3.one );          // Output { "x" : 1, "y" : 1, "z" : 1 }
JsonMapper.ToJson( Vector4.one );          // Output { "x" : 1, "y" : 1, "z" : 1, "w" : 1 }
JsonMapper.ToJson( Quaternion.identity );  // Output { "x" : 0, "y" : 0, "z" : 0, "w" : 0 }
JsonMapper.ToJson( Matrix4x4.zero );       // Output { "m33" : 0, .. }
JsonMapper.ToJson( Color.green );          // Output { "r" : 0, "g" : 1, "b" : 0, "a" : 1 }

JsonMapper.ToJson( Ray );                  // Output { "origin" : {V3}, "direction" : {V3} }
JsonMapper.ToJson( RaycastHit );           // Output { .. }
```
Of course reading back in also works:
```csharp
var v2 = JsonMapper.ToObject<Vector2>( "{\"x\":0,\"y\":0}" ); 
var v3 = JsonMapper.ToObject<Vector3>( "{\"x\":0,\"y\":0,\"z\":1}" ); 
..
```

#### float (Single) and long (Int64) types

 This fork includes [this patch](https://github.com/SONIC3D/litjson/commit/3cd16e3650f5f03765704b27700d4c3d37781a01.patch) for serializing float(Single) and long(Int64) types from this [pull request](https://github.com/lbv/litjson/pull/25) .


## Build with Mono Develop / Xamarin Studio / Visual Studio / ..

 1. Create a solution & Library project within your IDE and reference all files from ```/src/LitJson``` .
 2. Add a configuration called Unity3D ```Project > Options > Build > Compiler``` and add Define Symbol ```UNITY3D``` .
 3. Reference the UnityEngine.dll from your Unity installation folder .
 4. Build the project .


## Original README

 The original README did move to [README-ORIGINAL.md](README-ORIGINAL.md) containing make instructions and license information.

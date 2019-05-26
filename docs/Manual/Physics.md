# Physics

This asset utilizes Unity's built-in 3D physics.
You can add the regular `Rigidbody` & `Collider` components to your GameObject.

## Rigidbody

When adding the `Rigidbody` component make sure to check the _freeze rotation_ checkboxes in the inspector view.

![Shader](../images/freezeRotation.png)

You may also set these values from script 

```csharp hl_lines="4"
public void fooBar() {
    
   var rigidbody = gameObject.GetComponent<Rigidbody>();
    rigidbody.freezeRotation = true;   
}
```

for more information visit the [official Unity documentation](https://docs.unity3d.com/ScriptReference/Rigidbody-freezeRotation.html)

## Colliders

You can add any of the Unity 3D colliders to your GameObject. When a collider component is added Unity will set its size to match the sprite's bounds which most likely will be incorrect. Make sure to set the colliders size to the desired volume.
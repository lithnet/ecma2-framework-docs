# Creating single-file assemblies

When working with multiple management agents sharing the `Extensions` folder, it's important to create single-file assemblies to avoid conflicts and DLL overwriting. One recommended tool for achieving this is `Costura.Fody`.

## Using Costura.Fody

Costura.Fody is a library that embeds dependency DLLs into the main DLL as resources. At runtime, the dependency DLLs are extracted and loaded into memory. This approach preserves the original DLLs and is compatible with all types of assemblies.

However, there is a downside to this mechanism. When the MIM (Microsoft Identity Manager) interrogates your DLL, the dependency DLLs are not directly available to it. This can lead to errors when trying to load the DLL. To overcome this issue, you need to ensure that all public types in your assembly are marked as `internal`. By doing so, MIM will be able to work with the assembly without any issues.

To use Costura.Fody, you can add it via your NuGet package manager or add the following to your csproj project file:

```xml
<ItemGroup>
	<PackageReference Include="Costura.Fody" Version="5.7.0" PrivateAssets="all"/>
</ItemGroup>
```

## Troubleshooting
If your management agent DLL will not load when pressing the 'refresh interfaces' button on the MA configuration page, check the Application event log for more information.

If you see an exception message similar to the one below, then it is likely that you have one or more public types that are exposing a type from a third-party assembly that has been hidden by being embedded in the assembly.

```
The extensible extension returned an unsupported error.
 The stack trace is:
 
 "System.IO.FileNotFoundException: Could not load file or assembly 'Lithnet.Okta, Version=2.0.42.0, Culture=neutral, PublicKeyToken=null' or one of its dependencies. The system cannot find the file specified.
File name: 'Lithnet.Okta, Version=2.0.42.0, Culture=neutral, PublicKeyToken=null'
   at System.Reflection.RuntimeAssembly.GetExportedTypes(RuntimeAssembly assembly, ObjectHandleOnStack retTypes)
   at System.Reflection.RuntimeAssembly.GetExportedTypes()

Assembly manager loaded from:  C:\Windows\Microsoft.NET\Framework64\v4.0.30319\clr.dll
Running under executable  C:\Program Files\Microsoft Forefront Identity Manager\2010\Synchronization Service\Bin\miiserver.exe

```

Once again, make any public types in your DLL `internal` instead. Alternatively, if they must remain public, move them to another project, and reference them from the main project.

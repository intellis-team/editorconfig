# Intellis code style guide and `.editorconfig` file

## Tabs vs Spaces

We understand, agree with, and have deliberated considerably with both sides of this long ongoing debate. In some ways we fall on the side of using spacing for intentation.

However, where there is an option between tabs and spaces, we have settled on using tabs for indentation only for the sake of accessibility.  Tabs allows the individual developer to choose the size of the indentation of code in their own editor, which is important not only for preference.  A vision-impared developer, for example, may need to use a larger font size, and therefore a smaller indentation size.

Because we do consider it an accessbility concern, we ask all team members to comply with using tabs for indentation. All developers are free, however, to set the size of their tabs using their personal config in their editor of choice. Do not specify this in any shared configuration, such as an `.editorconfig` file within a project workspace.

This only applies to left-hand indentation.  When using spacing for formatting - such as for comment alignment, ascii art etc - spaces should be used after indenting using tabs, and care should be taken to ensure all lines that need to be aligned are using the same indentation.

Generally though, we discourage any formatting that relies on a fixed width font, which would include such formatting as above.

## Relevant formatting

```toml
[*]
indent_style = tab
```

## c# diagnostics and formatting

### File-scoped namespace declarations.

To reduce indentation, we use file-scoped namespace declarations

``` csharp
// File scoped namespace
namespace Intellis.Project;

class ClassName
{
}

// Avoid:
namespace Intellis.Project
{
  class ClassName
  {
  }
}
```
Declaration:

``` toml
csharp_style_namespace_declarations = file_scoped
```

## Implicit variable declaration

We prefer using var declarations where possible;

1. to avoid redundant code;
2. to reduce the need to hunt down a return type from external code;
3. and to generally create tidier code.

``` toml
csharp_style_var_for_built_in_types = true
csharp_style_var_when_type_is_apparent = true
csharp_style_var_elsewhere = true
```

### Async suffix

We don't enforce the use of an Async suffix for naming of Async functions, unless there are both async and non-async variations of the same function.

Typically, diagnostics will quickly pick up on erroneous usage.

``` toml
dotnet_diagnostic.VSTHRD200.severity = none
```

### ConfigureAwait()

As almost all of our internal dotnet code is written exclusively for use within web applications, there is little difference between the use of `ConfigureAwait(false)` and `ConfigureAwait(true)`.  Therefore we don't enforce the explicit use of either within our codebase.

``` toml
dotnet_diagnostic.VSTHRD111.severity = none
```

### High performance logging

Generally, the trade-off between the development overhead vs the performance improvements of using the LoggerMessage pattern is not sufficient for us to adhere to it in our projects, so we disable warnings about it

``` toml
dotnet_diagnostic.CA1848.severity = none
```

This does not mean, of course, that the LoggerMessage pattern should not be used in scenarios where performance is important.

## Yaml formatting

Yaml by specification requies spaces for indentation, therefore;

```toml
[*.yml, *.yaml]
indent_size = 2
indent_style = space
```



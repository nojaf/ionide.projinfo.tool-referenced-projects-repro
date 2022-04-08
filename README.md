# ionide.projinfo.tool referenced projects repro

## Steps to reproduce

* Clean checkout of this git repository.
* `dotnet tool restore`
* `dotnet proj-info --project .\Project1\Project1.fsproj`

Expected output (of Project1):
```
...
ReferencedProjects =
    [{ RelativePath = "..\Project2\Project2.fsproj"
       ProjectFileName =
        "C:\Users\nojaf\Projects\references-repro\Project2\Project2.fsproj"
       TargetFramework = "net6.0" }]
...
```

* Restore Project1. `dotnet restore .\Project1\Project1.fsproj`
* Run `proj-info` again, `dotnet proj-info --project .\Project1\Project1.fsproj`

Expected output (of Project1):

```
ReferencedProjects =
    [{ RelativePath = "..\Project2\Project2.fsproj"
       ProjectFileName =
        "C:\Users\nojaf\Projects\references-repro\Project2\Project2.fsproj"
       TargetFramework = "net6.0" };
     { RelativePath = "..\Project3\Project3.fsproj"
       ProjectFileName =
        "C:\Users\nojaf\Projects\references-repro\Project3\Project3.fsproj"
       TargetFramework = "net6.0" }]
```

`Project3` was added this time, because it is a reference of `Project2`.
This only appears when the `Projects` are restored.

Is this a bug or by design?
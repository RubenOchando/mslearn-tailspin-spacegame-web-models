Publish packages from external sources
Create a personal access token (PAT ulzdrhp6jneenjuiyf3xxabv7wd4gtr4qzo7l3w6fg4chon35ghq ) with packaging read and write scope.

Add your package source to your nuget.config file. This will add your PAT to your nuget.config file. Make sure to store this file in a safe place, and do not check this file into source control.

Command

Copy
dotnet nuget add source https://pkgs.dev.azure.com/<ORGANIZATION_NAME>/<PROJECT_NAME>/_packaging/<FEED_NAME>/nuget/v3/index.json --name <SOURCE_NAME> --username <USER_NAME> --password <PERSONAL_ACCESS_TOKEN> --configfile <PATH_TO_NUGET_CONFIG_FILE>
Publish your package:

Command

Copy
dotnet nuget push <PACKAGE_PATH> --source <SOURCE_NAME> --api-key <ANY_STRING>
Example:

Command

remember to do build of the PROJECT
and package with dotnet package
and move the package somewhere that path is the package path

Copy
dotnet nuget add source https://pkgs.dev.azure.com/ptrohWEorg/35ab38f2-3c5e-4a29-8a3a-7a43feff507b/_packaging/TailspinSpaceGameWebModels/nuget/v3/index.json --api-key "ptaz400"

dotnet nuget push --source "TailspinSpaceGameWebModels" --api-key TailSpinSpace "C:\LocalPackage\Tailspin.SpaceGame.Web.Models.1.0.0.nupkg" worked

https://pkgs.dev.azure.com/ptrohWEorg/35ab38f2-3c5e-4a29-8a3a-7a43feff507b/_packaging/TailspinSpaceGameWebModels/nuget/v3/index.json.


$ dotnet pack
MSBuild version 17.3.1+2badb37d1 for .NET
  Determining projects to restore...
  All projects are up-to-date for restore.
  Tailspin.SpaceGame.Web.Models -> C:\Users\ruoch\Documents\PT\Project\Learning\az-400\code\Space Game\mslearn-tailspin-spacegame-web-models\Tailspin.SpaceGame.Web.Models\bin\Debug\netstandard2.0\Tailspin.SpaceGa
  me.Web.Models.dll
  Successfully created package 'C:\Users\ruoch\Documents\PT\Project\Learning\az-400\code\Space Game\mslearn-tailspin-spacegame-web-models\Tailspin.SpaceGame.Web.Models\bin\Debug\Tailspin.SpaceGame.Web.Models.1.0.
  0.nupkg'.

  
$ dotnet nuget push --source "TailspinSpaceGameWebModels" --api-key TailSpinSpace "C:\LocalPackage\Tailspin.SpaceGame.Web.Models.1.0.0.nupkg"
Pushing Tailspin.SpaceGame.Web.Models.1.0.0.nupkg to 'https://pkgs.dev.azure.com/ptrohWEorg/35ab38f2-3c5e-4a29-8a3a-7a43feff507b/_packaging/16363733-dc1f-4115-bffe-34c719827ae9/nuget/v2/'...
  PUT https://pkgs.dev.azure.com/ptrohWEorg/35ab38f2-3c5e-4a29-8a3a-7a43feff507b/_packaging/16363733-dc1f-4115-bffe-34c719827ae9/nuget/v2/
  Accepted https://pkgs.dev.azure.com/ptrohWEorg/35ab38f2-3c5e-4a29-8a3a-7a43feff507b/_packaging/16363733-dc1f-4115-bffe-34c719827ae9/nuget/v2/ 4075ms
Your package was pushed.



pipeline rest
- task: DotNetCoreCLI@2
  displayName: 'Publish project'
  inputs:
      command: 'publish'
      publishWebProjects: false
      projects: '''**/*.csproj'''
- task: DotNetCoreCLI@2
  displayName: 'Push project'
  inputs:    
        command: 'push'
        packagesToPush: '$(Build.ArtifactStagingDirectory)/*.nupkg'
        nuGetFeedType: 'internal'
        publishVstsFeed: '6c793268-2bd0-4dc9-9c24-170546276b82'

        nuget.exe sources add -Name "TailspinSpaceGameWebModels" -Source "https://pkgs.dev.azure.com/ptrohWEorg/35ab38f2-3c5e-4a29-8a3a-7a43feff507b/_packaging/TailspinSpaceGameWebModels/nuget/v3/index.json" -username ruben ochando  -password ulzdrhp6jneenjuiyf3xxabv7wd4gtr4qzo7l3w6fg4chon35ghq
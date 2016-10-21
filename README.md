UnBuild : Unity Build configuration script
==========================================

BuildConfiguration
------------------
Use this class to ease creating and reusing build configurations, plus automating copying files to new builds.

Example:

    using UnBuild;
    using UnityEditor;
    
    public static class Builder {
    
        private static BuildConfiguration DefaultConfiguration {
            get {
                return new BuildConfiguration().SetExecName("CoolNewBuild")
                                               .AddScenes("Scenes/TestScene.unity");
            }
        }
    
        [MenuItem("Build/Test Build")]
        public static void CreateNewBuild() {
            Builder.DefaultConfiguration
                   .SetExecName("CoolNewBuild")
                   .SetTargetDir("../Builds/Test_" + Builder.CurrentTime)
                   .AddPostbuildCommandLine("echo Durum dum dum> durum.txt")
                   .AddBuildOptions(BuildOptions.Development, BuildOptions.ConnectWithProfiler)
                   .Build(BuildTarget.StandaloneWindows64);
        }
    
        private static string CurrentTime {
            get {
                System.DateTime now = System.DateTime.Now;
                string currentTime = string.Format("{0}{1:00}{2:00}_{3:00}{4:00}{5:00}",
                                                   now.Year,
                                                   now.Month,
                                                   now.Day,
                                                   now.Hour,
                                                   now.Minute,
                                                   now.Second);
                return currentTime;
            }
        }
    }

/*
 * Jakefile
 * EKSPinner
*/

var ENV = require("system").env,
    FILE = require("file"),
    JAKE = require("jake"),
    task = JAKE.task,
    FileList = JAKE.FileList,
    app = require("cappuccino/jake").app,
    configuration = ENV["CONFIG"] || ENV["CONFIGURATION"] || ENV["c"] || "Debug",
    OS = require("os");

app ("EKSPinner", function(task)
{
    task.setBuildIntermediatesPath(FILE.join(ENV["CAPP_BUILD"], "EKSPinner.build", configuration));
    task.setBuildPath(FILE.join(ENV["CAPP_BUILD"], configuration));

    task.setProductName("EKSPinner");
    task.setIdentifier("com.eliasklughammer.EKSpinner");
    task.setVersion("1.0");
    task.setAuthor("");
    task.setEmail("");
    task.setSummary("EKSPinner");
    task.setSources((new FileList("*.j")).exclude(FILE.join("Build", "**")));
    task.setResources(new FileList("Resources/*"));
    task.setInfoPlistPath("Info.plist");

    if (configuration === "Debug")
        task.setCompilerFlags("-DDEBUG -g");
    else
        task.setCompilerFlags("-O");
});

function printResults(configuration)
{
    print("----------------------------")
    print(configuration+" app built at path: "+FILE.join("Build", configuration, "EKSPinner"));
    print("----------------------------")
}

task ("default", ["EKSPinner"], function()
{
    printResults(configuration);
});

task ("build", ["default"]);

task ("install", ["debug", "release"])

task ("debug", function()
{
    ENV["CONFIGURATION"] = "Debug";
    JAKE.subjake(["."], "build", ENV);
});

task ("release", function()
{
    ENV["CONFIGURATION"] = "Release";
    JAKE.subjake(["."], "build", ENV);
});

task("test", function()
{
    var tests = new FileList('Tests/*Test.j');
    var cmd = ["ojtest"].concat(tests.items());
    var cmdString = cmd.map(OS.enquote).join(" ");

    var code = OS.system(cmdString);
    if (code !== 0)
        OS.exit(code);
});

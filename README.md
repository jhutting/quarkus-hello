# Minimal reproducible issue 9727

Follow the instructions [here](https://www.graalvm.org/latest/docs/getting-started/windows/) and install both [GraalVM 23](https://download.oracle.com/graalvm/23/latest/graalvm-jdk-23_windows-x64_bin.zip) and Visual Studio build tools/Windows SDK.

Set Path, JAVA_HOME and GRAALVM_HOME to GraalVM 23 folder.

## Creating a native executable

You can create a native executable using:

```shell script
./mvnw package -Dnative
```

This will now crash the build as described in [this issue](https://github.com/oracle/graal/issues/9727)

# Output
```
code-with-quarkus> .\mvnw.cmd package -Dnative
[INFO] Scanning for projects...
[INFO] 
[INFO] ---------------------< org.acme:code-with-quarkus >---------------------
[INFO] Building code-with-quarkus 1.0.0-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- resources:3.3.1:resources (default-resources) @ code-with-quarkus ---
[INFO] Copying 1 resource from src\main\resources to target\classes
[INFO] 
[INFO] --- quarkus:3.15.1:generate-code (default) @ code-with-quarkus ---
[INFO] 
[INFO] --- compiler:3.13.0:compile (default-compile) @ code-with-quarkus ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] 
[INFO] --- quarkus:3.15.1:generate-code-tests (default) @ code-with-quarkus ---
[INFO] 
[INFO] --- resources:3.3.1:testResources (default-testResources) @ code-with-quarkus ---
[INFO] skip non existing resourceDirectory C:\Projects\temp\code-with-quarkus\src\test\resources
[INFO]
[INFO] --- compiler:3.13.0:testCompile (default-testCompile) @ code-with-quarkus ---
[INFO] Nothing to compile - all classes are up to date.
[INFO]
[INFO] --- surefire:3.3.1:test (default-test) @ code-with-quarkus ---
[INFO] Using auto detected provider org.apache.maven.surefire.junitplatform.JUnitPlatformProvider
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running org.acme.GreetingResourceTest
2024-10-04 22:52:11,866 INFO  [io.quarkus] (main) code-with-quarkus 1.0.0-SNAPSHOT on JVM (powered by Quarkus 3.15.1) started in 2.530s. Listening on: http://localhost:8081
2024-10-04 22:52:11,868 INFO  [io.quarkus] (main) Profile test activated.
2024-10-04 22:52:11,868 INFO  [io.quarkus] (main) Installed features: [cdi, rest, smallrye-context-propagation, vertx]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 4.957 s -- in org.acme.GreetingResourceTest
2024-10-04 22:52:13,120 INFO  [io.quarkus] (main) code-with-quarkus stopped in 0.065s
[INFO] 
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO]
[INFO] --- jar:3.4.1:jar (default-jar) @ code-with-quarkus ---
[INFO] 
[INFO] --- quarkus:3.15.1:build (default) @ code-with-quarkus ---
[INFO] [io.quarkus.deployment.pkg.steps.JarResultBuildStep] Building native image source jar: C:\Projects\temp\code-with-quarkus\target\code-with-quarkus-1.0.0-SNAPSHOT-native-image-source-jar\code-with-quarkus-1.0.0-SNAPSHOT-runner.jar
[INFO] [io.quarkus.deployment.pkg.steps.NativeImageBuildStep] Building native image from C:\Projects\temp\code-with-quarkus\target\code-with-quarkus-1.0.0-SNAPSHOT-native-image-source-jar\code-with-quarkus-1.0.0-SNAPSHOT-runner.jar
[INFO] [io.quarkus.deployment.pkg.steps.NativeImageBuildStep] Running Quarkus native-image plugin on GRAALVM 24.1 JDK 23+37-jvmci-b01
[INFO] [io.quarkus.deployment.pkg.steps.NativeImageBuildRunner] C:\Progra~1\Java\graalvm-jdk-23+37.1\bin\native-image.cmd -J-Dlogging.initial-configurator.min-level=500 -J-Dsun.nio.ch.maxUpdateArraySize=100 -J-Djava.util.logging
.manager=org.jboss.logmanager.LogManager -J-Dio.netty.leakDetection.level=DISABLED -J-Dio.netty.allocator.maxOrder=3 -J-Dvertx.logger-delegate-factory-class-name=io.quarkus.vertx.core.runtime.VertxLogDelegateFactory -J-Dvertx.di
sableDnsResolver=true -J-Duser.language=en -J-Duser.country=US -J-Dfile.encoding=UTF-8 --features=io.quarkus.runner.Feature,io.quarkus.runtime.graal.DisableLoggingFeature -J--add-exports=java.security.jgss/sun.security.krb5=ALL-
UNNAMED -J--add-exports=java.security.jgss/sun.security.jgss=ALL-UNNAMED -J--add-opens=java.base/java.text=ALL-UNNAMED -J--add-opens=java.base/java.io=ALL-UNNAMED -J--add-opens=java.base/java.lang.invoke=ALL-UNNAMED -J--add-open
s=java.base/java.util=ALL-UNNAMED -H:+UnlockExperimentalVMOptions -H:BuildOutputJSONFile=code-with-quarkus-1.0.0-SNAPSHOT-runner-build-output-stats.json -H:-UnlockExperimentalVMOptions -H:+UnlockExperimentalVMOptions -H:+Generat
eBuildArtifactsFile -H:-UnlockExperimentalVMOptions -H:+UnlockExperimentalVMOptions -H:+AllowFoldMethods -H:-UnlockExperimentalVMOptions -J-Djava.awt.headless=true --no-fallback --link-at-build-time -H:+UnlockExperimentalVMOptio
ns -H:+ReportExceptionStackTraces -H:-UnlockExperimentalVMOptions -H:-AddAllCharsets --enable-url-protocols=http --enable-monitoring=heapdump -H:+UnlockExperimentalVMOptions -H:-UseServiceLoaderFeature -H:-UnlockExperimentalVMOp
tions -J--add-exports=org.graalvm.nativeimage/org.graalvm.nativeimage.impl=ALL-UNNAMED --exclude-config io\.netty\.netty-codec /META-INF/native-image/io\.netty/netty-codec/generated/handlers/reflect-config\.json --exclude-config io\.netty\.netty-handler /META-INF/native-image/io\.netty/netty-handler/generated/handlers/reflect-config\.json code-with-quarkus-1.0.0-SNAPSHOT-runner -jar code-with-quarkus-1.0.0-SNAPSHOT-runner.jar
Warning: Option 'DynamicProxyConfigurationResources' is deprecated and might be removed in a future release: This can be caused by a proxy-config.json file in your META-INF directory. Consider including proxy configuration in the reflection section of reachability-metadata.md instead.. Please refer to the GraalVM release notes.
========================================================================================================================
GraalVM Native Image: Generating 'code-with-quarkus-1.0.0-SNAPSHOT-runner' (executable)...
========================================================================================================================
For detailed information and explanations on the build output, visit:
https://github.com/oracle/graal/blob/master/docs/reference-manual/native-image/BuildOutput.md
------------------------------------------------------------------------------------------------------------------------
[1/8] Initializing...                                                                                    (8.6s @ 0.19GB)
 Java version: 23+37, vendor version: Oracle GraalVM 23+37.1
 Graal compiler: optimization level: 2, target machine: x86-64-v3, PGO: ML-inferred
 C compiler: cl.exe (microsoft, x64, 19.41.34120)
 Garbage collector: Serial GC (max heap size: 80% of RAM)
 3 user-specific feature(s):
 - com.oracle.svm.thirdparty.gson.GsonFeature
 - io.quarkus.runner.Feature: Auto-generated class by Quarkus from the existing extensions
 - io.quarkus.runtime.graal.DisableLoggingFeature: Disables INFO logging during the analysis phase
------------------------------------------------------------------------------------------------------------------------
 4 experimental option(s) unlocked:
 - '-H:+AllowFoldMethods' (origin(s): command line)
 - '-H:BuildOutputJSONFile' (origin(s): command line)
 - '-H:-UseServiceLoaderFeature' (origin(s): command line)
 - '-H:+GenerateBuildArtifactsFile' (origin(s): command line)
------------------------------------------------------------------------------------------------------------------------
Build resources:
 - 14.40GB of memory (60.1% of 23.94GB system memory, determined at start)
 - 4 thread(s) (100.0% of 4 available processor(s), determined at start)
[2/8] Performing analysis...  []                                                                        (20.9s @ 0.47GB)
    5,433 reachable types   (70.4% of    7,722 total)
    5,954 reachable fields  (37.7% of   15,798 total)
   23,745 reachable methods (40.2% of   59,072 total)
    1,886 types,    18 fields, and   429 methods registered for reflection
        3 native libraries: crypt32, ncrypt, psapi

Fatal error: com.oracle.graal.pointsto.util.AnalysisError$ParsingError: Error encountered while parsing jdk.internal.foreign.abi.DowncallStub/0x000000002424a400.invoke(Unknown Source)
Parsing context:
   at jdk.internal.org.jline.terminal.impl.ffm.Kernel32.GetConsoleScreenBufferInfo(Kernel32.java:224)
   at jdk.internal.org.jline.terminal.impl.ffm.WindowsAnsiWriter.getConsoleInfo(WindowsAnsiWriter.java:95)
   at jdk.internal.org.jline.terminal.impl.ffm.WindowsAnsiWriter.processEraseScreen(WindowsAnsiWriter.java:144)
   at jdk.internal.org.jline.utils.AnsiWriter.processEscapeCommand(AnsiWriter.java:291)
   at jdk.internal.org.jline.utils.AnsiWriter.write(AnsiWriter.java:134)
   at jdk.internal.org.jline.utils.AnsiWriter.write(AnsiWriter.java:781)
   at java.io.PrintWriter.implWrite(PrintWriter.java:621)
   at java.io.PrintWriter.write(PrintWriter.java:607)
   at java.io.PrintWriter.write(PrintWriter.java:635)
   at jdk.graal.compiler.util.json.JsonWriter.append(JsonWriter.java:128)
   at com.oracle.svm.enterprise.core.q.at(stripped:77)
   at com.oracle.svm.enterprise.core.t.execute(stripped:167)
   at com.oracle.svm.core.jdk.RuntimeSupport.executeHooks(RuntimeSupport.java:169)
   at com.oracle.svm.core.graal.snippets.CEntryPointSnippets.initializeIsolateInterruptibly1(CEntryPointSnippets.java:406)
   at com.oracle.svm.core.graal.snippets.CEntryPointSnippets.initializeIsolateInterruptibly0(CEntryPointSnippets.java:310)
   at com.oracle.svm.core.graal.snippets.CEntryPointSnippets.initializeIsolate(CEntryPointSnippets.java:294)
   at static root method.(Unknown Source)

        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.AnalysisError.parsingError(AnalysisError.java:165)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.createFlowsGraph(MethodTypeFlow.java:184)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.ensureFlowsGraphCreated(MethodTypeFlow.java:152)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.getOrCreateMethodFlowsGraphInfo(MethodTypeFlow.java:110)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.typestate.DefaultStaticInvokeTypeFlow.lambda$update$0(DefaultStaticInvokeTypeFlow.java:75)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.LightImmutableCollection.forEach(LightImmutableCollection.java:90)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.typestate.DefaultStaticInvokeTypeFlow.update(DefaultStaticInvokeTypeFlow.java:74)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.PointsToAnalysis$1.run(PointsToAnalysis.java:575)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.CompletionExecutor.executeCommand(CompletionExecutor.java:166)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.CompletionExecutor.lambda$executeService$0(CompletionExecutor.java:152)
        at java.base/java.util.concurrent.ForkJoinTask$RunnableExecuteAction.compute(ForkJoinTask.java:1726)
        at java.base/java.util.concurrent.ForkJoinTask$RunnableExecuteAction.compute(ForkJoinTask.java:1717)
        at java.base/java.util.concurrent.ForkJoinTask$InterruptibleTask.exec(ForkJoinTask.java:1641)
        at java.base/java.util.concurrent.ForkJoinTask.doExec(ForkJoinTask.java:507)
        at java.base/java.util.concurrent.ForkJoinPool$WorkQueue.topLevelExec(ForkJoinPool.java:1458)
        at java.base/java.util.concurrent.ForkJoinPool.runWorker(ForkJoinPool.java:2034)
        at java.base/java.util.concurrent.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:189)
Caused by: com.oracle.svm.core.util.VMError$HostedError: should not reach here: unexpected input could not be handled: linkToNative
        at org.graalvm.nativeimage.builder/com.oracle.svm.core.util.VMError.shouldNotReachHereUnexpectedInput(VMError.java:97)
        at org.graalvm.nativeimage.builder/com.oracle.svm.hosted.substitute.PolymorphicSignatureWrapperMethod.buildGraph(PolymorphicSignatureWrapperMethod.java:170)
        at org.graalvm.nativeimage.builder/com.oracle.svm.hosted.substitute.SubstitutionMethod.buildGraph(SubstitutionMethod.java:122)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.meta.AnalysisMethod.buildGraph(AnalysisMethod.java:657)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.AnalysisParsedGraph.parseBytecode(AnalysisParsedGraph.java:108)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.meta.AnalysisMethod.parseGraph(AnalysisMethod.java:916)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.meta.AnalysisMethod.ensureGraphParsedHelper(AnalysisMethod.java:881)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.meta.AnalysisMethod.ensureGraphParsed(AnalysisMethod.java:864)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.phases.InlineBeforeAnalysisGraphDecoder.lookupEncodedGraph(InlineBeforeAnalysisGraphDecoder.java:181)
        at jdk.graal.compiler/jdk.graal.compiler.replacements.PEGraphDecoder.doInline(PEGraphDecoder.java:1215)
        at jdk.graal.compiler/jdk.graal.compiler.replacements.PEGraphDecoder.tryInline(PEGraphDecoder.java:1198)
        at jdk.graal.compiler/jdk.graal.compiler.replacements.PEGraphDecoder.trySimplifyInvoke(PEGraphDecoder.java:1053)
        at jdk.graal.compiler/jdk.graal.compiler.replacements.PEGraphDecoder.handleInvokeWithCallTarget(PEGraphDecoder.java:1005)
        at jdk.graal.compiler/jdk.graal.compiler.replacements.PEGraphDecoder.handleInvoke(PEGraphDecoder.java:991)
        at jdk.graal.compiler/jdk.graal.compiler.nodes.GraphDecoder.processNextNode(GraphDecoder.java:926)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.phases.InlineBeforeAnalysisGraphDecoder.processNextNode(InlineBeforeAnalysisGraphDecoder.java:269)
        at jdk.graal.compiler/jdk.graal.compiler.nodes.GraphDecoder.decode(GraphDecoder.java:654)
        at jdk.graal.compiler/jdk.graal.compiler.replacements.PEGraphDecoder.decode(PEGraphDecoder.java:895)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.phases.InlineBeforeAnalysis.decodeGraph(InlineBeforeAnalysis.java:73)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlowBuilder.parse(MethodTypeFlowBuilder.java:200)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlowBuilder.apply(MethodTypeFlowBuilder.java:652)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.createFlowsGraph(MethodTypeFlow.java:167)
        ... 15 more
------------------------------------------------------------------------------------------------------------------------
                        1.0s (3.3% of total time) in 111 GCs | Peak RSS: 0.91GB | CPU load: 3.41
========================================================================================================================
Failed generating 'code-with-quarkus-1.0.0-SNAPSHOT-runner' after 30.5s.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  49.745 s
[INFO] Finished at: 2024-10-04T22:52:49+02:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal io.quarkus.platform:quarkus-maven-plugin:3.15.1:build (default) on project code-with-quarkus: Failed to build quarkus application: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
[ERROR]         [error]: Build step io.quarkus.deployment.pkg.steps.NativeImageBuildStep#build threw an exception: io.quarkus.deployment.pkg.steps.NativeImageBuildStep$ImageGenerationFailureException: Image generation failed. Exit code: 1
[ERROR]         at io.quarkus.deployment.pkg.steps.NativeImageBuildStep.imageGenerationFailed(NativeImageBuildStep.java:489)
[ERROR]         at io.quarkus.deployment.pkg.steps.NativeImageBuildStep.build(NativeImageBuildStep.java:278)
[ERROR]         at java.base/java.lang.invoke.MethodHandle.invokeWithArguments(MethodHandle.java:733)
[ERROR]         at io.quarkus.deployment.ExtensionLoader$3.execute(ExtensionLoader.java:856)
[ERROR]         at io.quarkus.builder.BuildContext.run(BuildContext.java:256)
[ERROR]         at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
[ERROR]         at org.jboss.threads.EnhancedQueueExecutor$Task.doRunWith(EnhancedQueueExecutor.java:2516)
[ERROR]         at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2495)
[ERROR]         at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1521)
[ERROR]         at java.base/java.lang.Thread.run(Thread.java:1575)
[ERROR]         at org.jboss.threads.JBossThread.run(JBossThread.java:483)
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoExecutionException
```
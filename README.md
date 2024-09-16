# repro

```shell
$ git diff 9523c2287284b912067ef3659ee179784a3b6a6a 0125d93d20e71620e851b2f2fe3bccf7d9082429
diff --git a/hello.py b/hello.py
index 8cde782..7f14c50 100644
--- a/hello.py
+++ b/hello.py
@@ -1 +1,2 @@
 print("hello world")
+print("hello world")

$ git checkout 9523c2287284b912067ef3659ee179784a3b6a6a
$ java -jar ~/bin/bazel-diff.jar generate-hashes -w $PWD --useCquery 9523c2287284b912067ef3659ee179784a3b6a6a.hashes

$ git checkout 0125d93d20e71620e851b2f2fe3bccf7d9082429
$ java -jar ~/bin/bazel-diff.jar generate-hashes -w $PWD --useCquery 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes

# shows no diff of the two hash files
$ diff -u 9523c2287284b912067ef3659ee179784a3b6a6a.hashes 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes

# generates an empty impacted-target file
$ java -jar ~/bin/bazel-diff.jar get-impacted-targets -sh 9523c2287284b912067ef3659ee179784a3b6a6a.hashes -fh 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes -o impacted-targets
```

# without `--useCquery`


```shell
$ git diff 9523c2287284b912067ef3659ee179784a3b6a6a 0125d93d20e71620e851b2f2fe3bccf7d9082429
diff --git a/hello.py b/hello.py
index 8cde782..7f14c50 100644
--- a/hello.py
+++ b/hello.py
@@ -1 +1,2 @@
 print("hello world")
+print("hello world")

$ git checkout 9523c2287284b912067ef3659ee179784a3b6a6a
$ java -jar ~/bin/bazel-diff.jar generate-hashes -w $PWD 9523c2287284b912067ef3659ee179784a3b6a6a.hashes

$ git checkout 0125d93d20e71620e851b2f2fe3bccf7d9082429
$ java -jar ~/bin/bazel-diff.jar generate-hashes -w $PWD 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes

$ diff -u 9523c2287284b912067ef3659ee179784a3b6a6a.hashes 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes
--- 9523c2287284b912067ef3659ee179784a3b6a6a.hashes	2024-09-16 12:21:39
+++ 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes	2024-09-16 12:21:55
@@ -18,7 +18,7 @@
   "//external:remote_jdk8_linux_s390x_toolchain_config_repo": "c8d941df0f1cfb26802cfd66f80228fd2124c5b2af0aab18e7e6b1dc13ba2976",
   "//external:remotejdk21_linux_ppc64le_toolchain_config_repo": "a24efb0aea42e05d1132844015dea96ce9e527b53edc08044582b4e51d8bb541",
   "//external:android/dx_jar_import": "12251c086f3b6553fbced8a1166c97b301731356da2462c3f9771e379620f05c",
-  "//:hello.py": "41cbbdf3c87356a40e34c07125518be6f6a943bfb3ca3f39fe7367742241b49f",
+  "//:hello.py": "39b57dcd8e616b68723e4898be5ad4214907aefc2ef256b6a41d7ea4a2a51177",
   "//external:remote_jdk8_linux": "04e8b8b45e941651cbb6ea0b7fb1660179fb46e1ec215f1b70b5112e5069c86d",
   "//external:remotejdk11_macos_aarch64": "0abebdd9e8914d42f8859d3171fb197199ffd6ff735be3a90f94a66540edc620",
   "//external:remotejdk17_win": "5e00ba2bfd36a279e48004e2c487928eba5bffc3b13df2f0714f8f2fc539363d",
\ No newline at end of file
@@ -65,7 +65,7 @@
   "//external:remotejdk17_macos_toolchain_config_repo": "31c251d6e5675a85b42c61d3e9b2eaef50a69e05d95ccb82cc73d7ba822a35df",
   "//external:remotejdk17_linux_ppc64le": "20de7e77d562e89d16030c2d77820de4e556495d3b537c63d2c74c253631d549",
   "//external:remote_jdk8_linux_s390x": "2a980b532da334f61a243bec6103734b7071569377c0ee12a7004672ba0f5baf",
-  "//:hello": "10e209cf8b8b3757135dfee4740a636bb5abb8599aab13455a6425ad8c673ffd",
+  "//:hello": "a9964b8e7060c2929a6bce46ce77c0f6490491cd63d725b922e87babf4c891f3",
   "//external:rules_license": "cdafb6738f896f32cd67cc54adb65b5c6e12709ccf9f9c98b7866208e33c55ac",
   "//external:remotejdk11_linux_s390x": "74f1dffa2cba3035d296ffaa5c51c8b40db9c4baf016e7da9cf6c3daadc13077",
   "//external:android_sdk_for_testing": "c487ef1981566938956d55d45b116dc55e3e9b6da439ffc991d5545828ee60da",
\ No newline at end of file

$ java -jar ~/bin/bazel-diff.jar get-impacted-targets -sh 9523c2287284b912067ef3659ee179784a3b6a6a.hashes -fh 0125d93d20e71620e851b2f2fe3bccf7d9082429.hashes -o impacted-targets
$ cat impacted-targets
//:hello.py
//:hello
```

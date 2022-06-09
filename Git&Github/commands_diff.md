# Git 명령어 - diff

- 어떤 내용이 수정이 되었는지 확인하기 위해 diff
#### diff 개념
```
git diff  // 아무 옵션이 없으면 working directory에 있는 것만 볼 수 있음
git diff --staged  // stage에 있는 것만 확인하고 싶을 때(staged 대신 cached도 사용 가능)
```
#### diff 결과
```
λ git diff --staged               
diff --git a/b.txt b/b.txt        
new file mode 100644              
index 0000000..12a8798            
--- /dev/null                     // 이전에는 아무 것도 없었는데       
+++ b/b.txt                       // b라는 파일이 추가가 되었다!      
@@ -0,0 +1 @@                     // -0,0 : 이전에는 어떤 줄도 없었지만 / +1 : 새로운 파일에는 첫 번째 줄에       
+hello world!                     // 'hello world!'가 추가되었다!    
diff --git a/style.css b/style.css  // staging area에는 style.css가 있어
new file mode 100644              
index 0000000..65699e6            
--- /dev/null                       // 이전에는 파일이 없었고
+++ b/style.css                     // 추가가 된 CSS 파일에는
@@ -0,0 +1 @@                       // -0,0 : 이전에는 어떤 줄도 없었지만 / +1 : 새로운 파일에는 첫 번째 줄에
+styling                            // 'styling'이라는 내용이 들어가있음!
```

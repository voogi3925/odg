---
{"dg-publish":true,"permalink":"/5-digital-garden/published/manuals/manual-how-to-use-server/","created":"2025-09-11T13:47:15.088+09:00"}
---


# Manual. How to use server

> 작성일: 2025-05-13

----
## Purpose of the post
- 서버 사용과 관련된 사항들을 기록해 정리해둔다.


------------
## External Link
- [2. C Shell 환경 및 사용 방법](http://coffeenix.net/doc/shell_programming/shell2.htm)


---------------
## tips
- 다른 서버에서 작업하다가 lock걸렸을 경우.
	- LOCK 풀기
		- library manager를 킨다 
		- 기존 터미널(mobaXterm이든 뭐든 서버 접속하고 있는 프로그램에서)에 'clsAdminTool'
		- 'are .' 입력으로 release edit locks (한칸 띄어쓰기 중요) 
		- 'ale .' 입력으로 결과 확인하기
		- 'quit' 로 나가기
- 권한 없음이 뜨는 경우 ("Permission Denied")
	- ls -al 로 파일 권한 확인
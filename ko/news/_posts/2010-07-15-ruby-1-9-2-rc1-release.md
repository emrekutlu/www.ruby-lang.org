---
layout: news_post
title: "Ruby 1.9.2 RC1 릴리즈"
author: "Moru"
lang: ko
---

Ruby 1.9.2 RC1이 릴리즈되었습니다. 이번 릴리즈는 1.9.2의 첫번째 릴리즈 후보입니다.

Ruby 1.9.2는 아래의 몇가지 항목을 제외하고, 1.9.1과의 호환성을 유지하고 있습니다.

* 다수의 추가 메소드
* 새로운 socket API(IPv6 지원)
* 새로운 인코딩
* 난수 생성을 위한 Random 클래스
* 새롭게 쓰여진 Time 클래스。2038년 문제가 해결됨.
* 몇 가지 정규식 확장
* $:는 현재 디렉토리를 포함하지 않도록 됨.
* dl은 libffi 상에서 새롭게 쓰여짐.
* libyaml의 wrapper인 psych 라이브러리. syck의 대용으로 사용가능.

자세한 사항은 [NEWS][1] 및 [ChangeLog][2]을 참조하여 주십시오.

Ruby 1.9.2 preview 3 이후 약 130건의 버그가 수정되었습니다. Ruby 1.9.2의 알려진 버그는
[#3462][3]를 제외하고 모두 수정되었습니다.

Ruby 1.9.2은 8월초 릴리즈될 예정입니다. 1.9.2 릴리즈 스케쥴은 RubySpec 호환성을 위해 취소된 적이 있으나,
현재는 RubySpec 99%의 호환성을 보장하고 있습니다.

사용중 문제가 발생하였을 때에는 [Ruby Issue Tracking System][4]을 통해 문제점을 알려주시기 바랍니다.

### 

* [&lt;URL:http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-rc1.tar.bz2&gt;][5]
  
  : 8479087 bytes
  
  
  : 242dcfaed8359a6918941b55d0806bf0
  
  
  : c2a680aa5472c8d04a71625afa2b0f75c030d3655a3063fe364cfda8b33c1480

* [&lt;URL:http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-rc1.tar.gz&gt;][6]
  
  : 10779309 bytes
  
  
  : fdedd5b42ae89a9a46797823ad2d9acf
  
  
  : 3e90036728342ce8463be00d42d4a36de70dabed96216c5f8a26ec9ba4b29537

* [&lt;URL:http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-rc1.zip&gt;][7]
  
  : 12158992 bytes
  
  
  : 3da59c5d3567f6e1f1697abbef71f507
  
  
  : 4f593a3d0873cea8f371a7fc7484cad7bc03acac0ada1970cb9f83a89bc27997



[1]: http://svn.ruby-lang.org/repos/ruby/tags/v1_9_2_rc1/NEWS 
[2]: http://svn.ruby-lang.org/repos/ruby/tags/v1_9_2_rc1/ChangeLog 
[3]: http://redmine.ruby-lang.org/issues/show/3462 
[4]: http://redmine.ruby-lang.org/projects/show/ruby-19/ 
[5]: http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-rc1.tar.bz2 
[6]: http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-rc1.tar.gz 
[7]: http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.2-rc1.zip 
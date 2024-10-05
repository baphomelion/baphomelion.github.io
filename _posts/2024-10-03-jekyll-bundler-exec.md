---
title: "jekyll bundle exec error"
categories:
  - Blog
tags:
  - bundler
  - error
toc: true
---

## 문제
jekyll build 시 아래 메시지와 함께 Gem::LoadError 에러 발생
```
You have already activated public_suffix 6.0.1, but your Gemfile requires public_suffix 5.1.1.
Prepending `bundle exec` to your command may solve this. 
```

## 원인
Ruby 환경에서 설치된 Gem 버전과 Gemfile에서 요구하는 버전이 충돌

## 해결 방법 1
명령어 앞에 bunlder exec 추가하여 Gemfile에 지정된 버전을 사용
```
# bundler exec jekyll serve
```

## 해결 방법 2
모든 Gem 삭제 후 Gemfile에 맞는 버전으로 재설치

### 삭제

```
# gem list | %{$_.split(' ')[0]} | %{gem uninstall -Iax $_ }
```
```
Gem abbrev-0.1.2 cannot be uninstalled because it is a default gem
Successfully uninstalled activesupport-7.2.1
Successfully uninstalled addressable-2.8.7
Successfully uninstalled base64-0.2.0
There was both a regular copy and a default copy of base64-0.2.0. The regular copy was successfully uninstalled, but the default copy was left around because default gems can't be removed.
Gem benchmark-0.3.0 cannot be uninstalled because it is a default gem
Gem bigdecimal-3.1.5 cannot be uninstalled because it is a default gem
Successfully uninstalled bigdecimal-3.1.8
Gem bundler-2.5.16 cannot be uninstalled because it is a default gem
...
Successfully uninstalled webrick-1.8.2
Gem win32ole-1.8.10 cannot be uninstalled because it is a default gem
Gem yaml-0.3.0 cannot be uninstalled because it is a default gem
Gem zlib-3.1.1 cannot be uninstalled because it is a default gem
```

### 재설치
```
# bundler install
```
```
Bundler 2.5.16 is running, but your lockfile was generated with 2.5.20. Installing Bundler 2.5.20 and restarting using that version.
Fetching gem metadata from https://rubygems.org/.
Fetching bundler 2.5.20
Installing bundler 2.5.20
Fetching gem metadata from https://rubygems.org/.........
...
Please ensure that your Gemfiles and .gemspecs are suitably restrictive
to avoid an unexpected breakage when 3.0 is released (e.g. ~> 2.3.0).
See https://github.com/rubyzip/rubyzip for details. The Changelog also
lists other enhancements and bugfixes that have been implemented since
version 2.3.0.
```

### 확인
```
# jekyll serve
```
```
Configuration file: Z:/repository/baphomelion.github.io/_config.yml
C:/Ruby33-x64/lib/ruby/3.3.0/win32/registry.rb:2: warning: fiddle was loaded from the standard library, but will no longer be part of the default gems starting from Ruby 3.5.0.
You can add fiddle to your Gemfile or gemspec to silence this warning.
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
            Source: Z:/repository/baphomelion.github.io
       Destination: Z:/repository/baphomelion.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.215 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'Z:/repository/baphomelion.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```
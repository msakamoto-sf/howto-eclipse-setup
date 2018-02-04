# howto-eclipse-setup

Eclipse Setup How-To and some configuration files (cleanup, formatter, ...)

This is copy of SecureSkyTechnology/howto-eclipse-setup :
- `master` : sync to upstream (SecureSkyTechnology/howto-eclipse-setup) main branch.
- `msakamoto-sf-custom` : my customized contents. (github default)

how to sync master branch from upstream :
```
git remote add upstream https://github.com/SecureSkyTechnology/howto-eclipse-setup.git
or
git remote add upstream git@github.com:SecureSkyTechnology/howto-eclipse-setup.git

git remote -v
(check "upstream" registration)

git fetch upstream

git checkout master

git merge upstream/master
```

About syncing upstream branch reference:
- Configuring a remote for a fork - User Documentation
  - https://help.github.com/articles/configuring-a-remote-for-a-fork/
- Syncing a fork - User Documentation
  - https://help.github.com/articles/syncing-a-fork/
- GitHubでFork/cloneしたリポジトリを本家リポジトリに追従する - Qiita
  - https://qiita.com/xtetsuji/items/555a1ef19ed21ee42873
- Github で Fork してから Pull Request をするまでの流れ | けーこ in サンフランシスコ
  - http://kik.xii.jp/archives/179
- Githubでforkしたリポジトリでオリジナルリポジトリの変更を追従する - dev.toihrk.me
  - http://dev.toihrk.me/2015/06/02/github-fork-usage.html
- github で fork したリポジトリで本家に追従する - Please Sleep
  - http://please-sleep.cou929.nu/track-original-at-forked-repo.html


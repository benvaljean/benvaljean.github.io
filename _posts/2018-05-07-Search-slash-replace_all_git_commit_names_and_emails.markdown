---
layout: post 
title: Search/replace all git commit names and emails
---

Search for all git commits in all branches where comitter email is
wrong\@example.com and reweite the commit to match a name of Golide and
an email of correct\@address.com

This should only be used for private repos as you are rewritig history.

    $ git filter-branch --env-filter '
    WRONG_EMAIL="wrong@example.com"
    NEW_NAME="Golide"
    NEW_EMAIL="correct@address.com"

    if [ "$GIT_COMMITTER_EMAIL" = "$WRONG_EMAIL" ]
    then
        export GIT_COMMITTER_NAME="$NEW_NAME"
        export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
    fi
    if [ "$GIT_AUTHOR_EMAIL" = "$WRONG_EMAIL" ]
    then
        export GIT_AUTHOR_NAME="$NEW_NAME"
        export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
    fi
    ' --tag-name-filter cat -- --branches --tags

References:
<https://www.git-tower.com/learn/git/faq/change-author-name-email>

[Category:Git](Category:Git "wikilink")

# Örnek Konfigürasyon Dosyası

Bu örneği kendinize göre düzenleyip `~/.gitconfig` olarak kullanabilirsiniz.

    [user]
        name = AD SOYAD
        email = E-POSTA
    [commit]
        template = ~/.git-commit-template
    [alias]
        add-modified            = !"git status -sb | grep '^ M ' | sed 's/ M //' | xargs git add"
        add-untracked           = !"git status -sb | grep '^??' | sed 's/?? //' | sed 's/.*/\"&\"/' | xargs git add"
        branches                = for-each-ref --sort=-committerdate --format='%(color:white)[%(refname:short):%(color:yellow)%(objectname:short)%(color:reset)]%(color:reset) \t %(color:red)%(authorname)%(color:reset) \t %(color:blue)%(authordate:relative)%(color:reset)' refs/remotes
        show-ignored            = "ls-files -o -i --exclude-standard"
        show-todays-diff        = "diff --shortstat '@{0 day ago}'"
        show-untracked          = "ls-files --others --exclude-standard"
        add-deleted             = "add -u"
        root-commit             = "rev-list --max-parents=0 HEAD"
        next-commit             = !"git checkout $(git log --reverse --ancestry-path --pretty=%H HEAD..master | head -1)"
        unstage                 = "reset HEAD --"
        uncommit                = "reset --soft HEAD^"
        wip                     = !"git add -A; git ls-files --deleted -z | xargs -0 git rm; git commit -m 'wip'"
        initial-commit-tr       = "commit --allow-empty -m'[root] İlk commit'"
        initial-commit          = "commit --allow-empty -m'[root] Initial commit'"
        br                      = "branch -v"
        bra                     = "branch -avv"
        brd                     = "branch -d"
        brm                     = "branch --no-mergedd"
        brnm                    = "branch --no-merged"
        brr                     = "branch -rv"
        ci                      = "commit"
        co                      = "checkout"
        df                      = "diff --word-diff"
        dfn                     = "diff --name-only"
        fc                      = "commit --allow-empty -m"
        lg                      = "log --graph --decorate --oneline --all"
        lg2                     = "log --graph --decorate --pretty='%C(auto)%h %G?%d %C(white)%s%C(reset) [%aE, %ad]' --date=relative"
        lgs                     = "log --graph --decorate --oneline"
        list-remote-tags        = "ls-remote --tags"
        ls                      = "ls-files"
        pullr                   = "pull --rebase"
        rmt                     = "remote -v"
        st                      = "status"
        stu                     = "status --untracked-files"
        sti                     = "status --ignored"
        sts                     = "status -sb"
        track-origin-master     = "branch --set-upstream-to=origin/master master"
    [color]
        ui = auto
    [color "branch"]
        current = yellow reverse
        local = yellow
        remote = green
    [color "diff"]
        meta = yellow bold
        frag = magenta bold
        old = red bold
        new = green bold
    [color "status"]
        added = yellow bold
        changed = green
        untracked = red
    [core]
        excludesfile = ~/.gitignore
        whitespace = fix,-indent-with-non-tab,trailing-space,cr-at-eol
        pager = less -FRX
        autocrlf = input
        safecrlf = true
        disambiguate = commit
        abbrev = 12
    [push]
        default = tracking
    [filter "media"]
        clean = git-media-clean %f
        smudge = git-media-smudge %f
    [pull]
        rebase = true
    [fetch]
        prune = true
    [rerere]
        enabled = true
    [help]
        autocorrect = 0
    [diff]
        compactionHeuristic = 1
    [status]
    	submoduleSummary = true

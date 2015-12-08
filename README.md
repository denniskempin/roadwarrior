# RoadWarrior
Handy little tool to work remotely on large code bases.

RoadWarrior wraps around rsync and provides an easy workflow to check out multiple folders from a remote server, then watch those checked out folders for changes and sync them back.

Why? It's fast, it's happening automatically in the background and you can continue to work offline and sync back changes after getting back online.

Install

    $ pip install roadwarrior

Put a roadwarrior.yaml config file into any empty folder of your choice.

    $ cat roadwarrior.yaml
    remote: my_remote_host:/workspace
    mapping:
      components: chromium/src/components/
      ui: chromium/src/ui

The 'mapping' maps local folders to remote folders.
A checkout with roadwarrior will sync down all files from the remote folders.

    $ roadwarrior -c (or --checkout)
    my_remote_host:/workspace/chromium/src/components/  ->  ./components/
    my_remote_host:/workspace/chromium/src/ui/  ->  ./ui/
    $ ls
    components ui

Watch local folders for changes and update remote instantly:

    $ roadwarrior -w (or --watch)
    Watching...
    (change a file)
    Push ./ui/README.chromium

# Why not SSHFS/Samba/NFS?
On large projects, working via a remote file system can be painfully slow and error prone. Especially using editors or IDEs that index files or watch for file changes can degrade performance significantly.
Saving files on a poor connection can freeze the UI and you have to manually copy files if you want to keep them to work offline.

# Why not GIT?
GIT is not always an option when the project is already on GIT and you do not want to check out the whole source tree. Also the workflow does not work well when you want to do quick and small iterations with compilation or test runs on the remote host.

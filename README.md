This charm is to demonstrate a problem I'm experiencing with adding a git
source to my `charmcraft.yaml`. The problem can be reproduced by cloning this
branch and running `charmcraft pack`, which will produce output as follows:
```
# From log of charmcraft output
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.724 Found installed version 1:2.34.1-1ubuntu1.9 for package git
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.724 Found installed version 1:2.34.1-1ubuntu1.9 for package git-man
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.724 Found installed version 7.81.0-1ubuntu1.10 for package libcurl3-gnutls
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.724 Found installed version 0.17029-1 for package liberror-perl
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.726 verify plugin environment for part 'git-stuff'
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.727 Running step PULL for part 'git-stuff'
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.727 Execute action
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.728 execute action git-stuff:Action(part_name='git-stuff', step=Step.PULL, action_type=ActionType.RUN, reason=None, project_vars=None, properties=ActionProperties(changed_files=None, changed_dirs=None))
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.728 Executing: git clone --recursive --branch master --depth 1 https://git.launchpad.net/juju-upgrader
2023-05-06 14:43:01.946 :: 2023-05-06 12:42:56.731 :: Cloning into '/root/parts/git-stuff/src'...
2023-05-06 14:43:01.946 :: 2023-05-06 12:43:01.708 :: usage: git submodule [--quiet] [--cached]
2023-05-06 14:43:01.946 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] add [-b <branch>] [-f|--force] [--name <name>] [--reference <repository>] [--] <repository> [<path>]
2023-05-06 14:43:01.946 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] status [--cached] [--recursive] [--] [<path>...]
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] init [--] [<path>...]
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] deinit [-f|--force] (--all| [--] <path>...)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] update [--init] [--remote] [-N|--no-fetch] [-f|--force] [--checkout|--merge|--rebase] [--[no-]recommend-shallow] [--reference <repository>] [--recursive] [--] [<path>...]
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] set-branch (--default|--branch <branch>) [--] <path>
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] set-url [--] <path> <newurl>
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] summary [--cached|--files] [--summary-limit <n>] [commit] [--] [<path>...]
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] foreach [--recursive] <command>
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] sync [--recursive] [--] [<path>...]
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.708 :: or: git submodule [--quiet] absorbgitdirs [--] [<path>...]
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.709 Parts processing error: Failed to pull source: command ['git', 'clone', '--recursive', '--branch', 'master', '--depth', '1', 'https://git.launchpad.net/juju-upgrader', '/root/parts/git-stuff/src'] exited with code 1.
2023-05-06 14:43:01.947 :: Make sure sources are correctly specified.
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712 Traceback (most recent call last):
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/sources/base.py", line 131, in _run
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     os_utils.process_run(command, logger.debug, **kwargs)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/utils/os_utils.py", line 347, in process_run
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     raise subprocess.CalledProcessError(ret, command)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712 subprocess.CalledProcessError: Command '['git', 'clone', '--recursive', '--branch', 'master', '--depth', '1', 'https://git.launchpad.net/juju-upgrader', '/root/parts/git-stuff/src']' returned non-zero exit status 1.
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712 During handling of the above exception, another exception occurred:
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712 Traceback (most recent call last):
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/charmcraft/parts.py", line 468, in run
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     aex.execute([act], stdout=stream, stderr=stream)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/executor.py", line 304, in execute
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     self._executor.execute(actions, stdout=stdout, stderr=stderr)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/executor.py", line 128, in execute
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     self._run_action(act, stdout=stdout, stderr=stderr)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/executor.py", line 193, in _run_action
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     handler.run_action(action, stdout=stdout, stderr=stderr)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/part_handler.py", line 172, in run_action
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     state = handler(step_info, stdout=stdout, stderr=stderr)
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/part_handler.py", line 198, in _run_pull
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     self._run_step(
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/part_handler.py", line 493, in _run_step
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     return step_handler.run_builtin()
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712   File "/snap/charmcraft/1349/lib/craft_parts/executor/step_handler.py", line 106, in run_builtin
2023-05-06 14:43:01.947 :: 2023-05-06 12:43:01.712     return handler()

# However, we can see that the code has actually been downloaded:

mthaddon@finistere:~/Documents/tmp/charmcraft-git-test$ lxc start --project charmcraft charmcraft-charmcraft-git-test-4047355-0-0-amd64 
mthaddon@finistere:~/Documents/tmp/charmcraft-git-test$ lxc exec --project charmcraft charmcraft-charmcraft-git-test-4047355-0-0-amd64 su -
root@charmcraft-charmcraft-git-test-4047355-0-0-amd64:~# cd /root/parts/git-stuff/src/
root@charmcraft-charmcraft-git-test-4047355-0-0-amd64:~/parts/git-stuff/src# ls
COPYING   README.md  juju-check          juju-upgrader        juju_formatter.py   juju_status.py  pytest.ini        tox.ini
Makefile  TODO       juju-machine-check  juju_diagnostics.py  juju_statistics.py  juju_utils.py   requirements.txt  unit_tests
root@charmcraft-charmcraft-git-test-4047355-0-0-amd64:~/parts/git-stuff/src# git remote -v
origin  https://git.launchpad.net/juju-upgrader (fetch)
origin  https://git.launchpad.net/juju-upgrader (push)
root@charmcraft-charmcraft-git-test-4047355-0-0-amd64:~/parts/git-stuff/src# git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
root@charmcraft-charmcraft-git-test-4047355-0-0-amd64:~/parts/git-stuff/src# 

```

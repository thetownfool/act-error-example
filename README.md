# Dry run results in RTE for a simple pipeline.

running `act -n` against provided [sample](https://github.com/thetownfool/act-error-example), results in the following exception:

```shell

panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x71 pc=0x164e10e]

goroutine 5 [running]:
github.com/docker/docker/client.(*Client).getAPIPath(0xc0003ebb90?, {0x19841f8?, 0xc0004337a0?}, {0xc0000f33c0, 0x14}, 0x14?)
	/Users/brew/Library/Caches/Homebrew/go_mod_cache/pkg/mod/github.com/docker/docker@v20.10.13+incompatible/client/client.go:183 +0x4e
github.com/docker/docker/client.(*Client).sendRequest(0x1856eb7?, {0x19841f8, 0xc0004337a0}, {0x18568aa, 0x3}, {0xc0000f33c0?, 0x80000000a?}, 0x49249249249249?, {0x0, 0x0}, ...)
	/Users/brew/Library/Caches/Homebrew/go_mod_cache/pkg/mod/github.com/docker/docker@v20.10.13+incompatible/client/request.go:109 +0x78
github.com/docker/docker/client.(*Client).get(...)
	/Users/brew/Library/Caches/Homebrew/go_mod_cache/pkg/mod/github.com/docker/docker@v20.10.13+incompatible/client/request.go:37
github.com/docker/docker/client.(*Client).CopyFromContainer(0x56?, {0x19841f8, 0xc0004337a0}, {0x0, 0x0}, {0xc0004800c0, 0x56})
	/Users/brew/Library/Caches/Homebrew/go_mod_cache/pkg/mod/github.com/docker/docker@v20.10.13+incompatible/client/container_copy.go:68 +0x1fe
github.com/nektos/act/pkg/container.(*containerReference).GetContainerArchive(0xc0000f3798?, {0x19841f8?, 0xc0004337a0?}, {0xc0004800c0?, 0xc0000f37a0?})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/container/docker_run.go:164 +0x59
github.com/nektos/act/pkg/runner.(*StepContext).Executor.func1.1({0x185a42b?, 0xc0000f3888?})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/step_context.go:70 +0xbc
github.com/nektos/act/pkg/runner.(*StepContext).readAction(0x19841f8?, 0xc0001e3500, {0xc00016fcc0, 0x4b}, {0x0, 0x0}, 0xc00010ebd0, 0x18b2898)
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/action.go:25 +0x9c
github.com/nektos/act/pkg/runner.(*StepContext).setupAction.func1({0x19841f8?, 0xc0004337a0?})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/step_context.go:387 +0x9f
github.com/nektos/act/pkg/common.Executor.Then.func1({0x19841f8, 0xc0004337a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:131 +0x34
github.com/nektos/act/pkg/runner.(*RunContext).newStepExecutor.func1({0x19841f8, 0xc0004337a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/run_context.go:360 +0x350
github.com/nektos/act/pkg/runner.newJobExecutor.func2.1(0x19841f8?, {0x19841f8, 0xc0004337a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/job_executor.go:42 +0x36
github.com/nektos/act/pkg/runner.newJobExecutor.func2({0x19841f8?, 0xc00010e2a0?})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/job_executor.go:51 +0x8d
github.com/nektos/act/pkg/common.Executor.Then.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:143 +0xe4
github.com/nektos/act/pkg/common.Executor.Then.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:131 +0x34
github.com/nektos/act/pkg/common.Executor.Then.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:131 +0x34
github.com/nektos/act/pkg/common.Executor.Then.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:131 +0x34
github.com/nektos/act/pkg/common.Executor.Finally.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:177 +0x34
github.com/nektos/act/pkg/common.Executor.Finally.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:177 +0x34
github.com/nektos/act/pkg/runner.(*RunContext).Executor.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/run_context.go:290 +0x67
github.com/nektos/act/pkg/common.Executor.Finally.func1({0x19841f8, 0xc00010e2a0})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:177 +0x34
github.com/nektos/act/pkg/runner.(*runnerImpl).NewPlanExecutor.func1.1({0x19841f8, 0xc000432450})
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/runner/runner.go:171 +0x2f2
github.com/nektos/act/pkg/common.NewParallelExecutor.func1.1(0x0?, 0x0?)
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:102 +0x5c
created by github.com/nektos/act/pkg/common.NewParallelExecutor.func1
	/private/tmp/act-20220322-14079-18pjzcc/act-0.2.26/pkg/common/executor.go:100 +0x89
```

`act --bug-report` :

```shell
act version:            0.2.26
GOOS:                   darwin
GOARCH:                 amd64
NumCPU:                 8
Docker host:            DOCKER_HOST environment variable is unset/empty.
Sockets found:
	/var/run/docker.sock
Config files:
	/Users/carl/.actrc:
		-P ubuntu-latest=ghcr.io/catthehacker/ubuntu:act-latest
		-P ubuntu-20.04=ghcr.io/catthehacker/ubuntu:act-20.04
		-P ubuntu-18.04=ghcr.io/catthehacker/ubuntu:act-18.04
Docker Engine:
	Engine version:        20.10.8
	Engine runtime:        runc
	Cgroup version:        1
	Cgroup driver:         cgroupfs
	Storage driver:        overlay2
	Registry URI:          https://index.docker.io/v1/
	OS:                    Docker Desktop
	OS type:               linux
	OS version:
	OS arch:               x86_64
	OS kernel:             5.10.47-linuxkit
	OS CPU:                4
	OS memory:             1985 MB
	Security options:
		name=seccomp,profile=default
```
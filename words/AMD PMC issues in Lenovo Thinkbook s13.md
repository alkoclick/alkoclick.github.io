#ubuntu #linux 

Trying to get suspend and hibernate working on my [[Lenovo Thinkbook s13]]

Trying to use suspend from the [[ACPI Power States]] `systemctl suspend` (to be fair this is s2idle, which is one of the [[S0ix states]]) failed and led to a black screen:

```
Feb 12 12:04:47 alexbot-ThinkBook-13s systemd[1]: Finished GRUB failed boot detection.
░░ Subject: A start job for unit grub-initrd-fallback.service has finished successfully
░░ Defined-By: systemd
░░ Support: [http://www.ubuntu.com/support](http://www.ubuntu.com/support)
░░ 
░░ A start job for unit grub-initrd-fallback.service has finished successfully.
░░ 
░░ The job identifier is 2387.
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: Freezing user space processes ... (elapsed 0.002 seconds) done.
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: OOM killer disabled.
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: Freezing remaining freezable tasks ... (elapsed 0.001 seconds) done.
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: printk: Suspending console(s) (use no_console_suspend to debug)
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: amd_pmc AMDI0005:00: SMU response timed out
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: amd_pmc AMDI0005:00: failed to talk to SMU
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: amd_pmc AMDI0005:00: failed to talk to SMU
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: amd_pmc AMDI0005:00: suspend failed
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: PM: dpm_run_callback(): acpi_subsys_suspend_noirq+0x0/0x50 returns -110
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: amd_pmc AMDI0005:00: PM: failed to suspend noirq: error -110
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: PM: noirq suspend of devices failed
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: pci 0000:00:00.2: can't derive routing for PCI INT A
Feb 12 12:04:53 alexbot-ThinkBook-13s kernel: pci 0000:00:00.2: PCI INT A: no GSI

```

Installed [[Powertop]] and calibrated, which took about 10m but all the "proper" switches were already set correctly. Didn't do much more with it and eventually uninstalled.

I downloaded the updated 5.14 kernel that should have the hotfix: [https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.14.21/amd64/](https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.14.21/amd64/)

Still had the SMU timeout, so I tried to go to 5.15, which is what ubuntu 22.04 will use anyway: [https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.15.23/amd64/](https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.15.23/amd64/)

In 5.15, on my first or second suspend I hit: `[amdgpu]] *ERROR* Error scheduling IBs`

```
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: [drm:amdgpu_ring_test_helper [amdgpu]] *ERROR* ring sdma0 test failed (-110)
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: [drm:amdgpu_device_ip_resume_phase2 [amdgpu]] *ERROR* resume of IP block <sdma_v4_0> failed -110
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: amdgpu: amdgpu_device_ip_resume failed (-110).
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: PM: dpm_run_callback(): pci_pm_resume+0x0/0xf0 returns -110
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: PM: failed to resume async: error -110


Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: amdgpu: couldn't schedule ib on ring <sdma0>
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: [drm:amdgpu_job_run [amdgpu]] *ERROR* Error scheduling IBs (-22)
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: amdgpu: couldn't schedule ib on ring <sdma0>
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: [drm:amdgpu_job_run [amdgpu]] *ERROR* Error scheduling IBs (-22)
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: amdgpu: couldn't schedule ib on ring <sdma0>
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: [drm:amdgpu_job_run [amdgpu]] *ERROR* Error scheduling IBs (-22)
Feb 12 13:04:41 alexbot-ThinkBook-13s kernel: amdgpu 0000:03:00.0: amdgpu: couldn't schedule ib on ring <sdma0>

```

[https://bugs.launchpad.net/amd/+bug/1943633](https://bugs.launchpad.net/amd/+bug/1943633)

After all of this, I had issues because suspend-then-hibernate would not engage properly: Suspend worked, but even with a 60s delay, it wouldn't go into hibernate. However, as soon as I opened the screen, it would immediately wake, then go into hibernate. Smh.

I modified my `/etc/systemd/sleep.conf.d/99updates.conf` and `/etc/systemd/logind.conf`

I tried replacing the target of suspend with suspend-then-hibernate as described in [this SO answer](https://askubuntu.com/questions/1316120/cannot-set-the-system-to-automatically-suspend-and-then-hibernat-when-closing-th)

It seems to have actually worked!
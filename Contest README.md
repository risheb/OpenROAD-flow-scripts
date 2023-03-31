# OpenROAD Flow

OpenROAD Flow is a full RTL-to-GDS flow built entirely on open-source tools.
The project aims for automated, no-human-in-the-loop digital circuit design
with 24-hour turnaround time.

## The OpenROAD 7nm Physical Design Contest

This contest, organized by The OpenROAD Project and VSD, features interesting design challenges at an advanced technology node (7nm).Following are the problem statement for this contest.
1. Problem A (Best Performance):
Using any of the following RISC-V cores from the OpenROAD-flow-scripts repository: RISCV32i, ibex, swerv_wrapper demonstrate the best achievable performance for the design for a given die size on ASAP7. The design must be DRC and LVS clean.

2. Problem B (Best Possible Runtime):
Using any of the following RISC-V cores from the OpenROAD flow-scripts repository: RISC-V32i, ibex, swerv_wrapper demonstrate the fastest Runtime from RTL-GDSII with good area and performance. Use cloud resources, suitable design configurations, tool changes (any or all of these) to meet this target. The design must be DRC and LVS clean.

## Chosen problem for contest

For this contest, problem A was the main focus at the same time, try to improve PPA for ibex design using ASAP7 platform.

# Updates Made For This Contest:

For the purpose of this contest, ORFS was installed locally However, there was issues faced during installation. For this perpose, a change is made in source file.

## 1. Installation update

By default, -m64 is flagged in OpenROAD/src/par/CMakeList.txt. This prevents users with ARM64 architecture from installing the OpenROAD software using build_openroad.sh. To avoid this, the flag is removed and user can now install OpenROAD software using build_openroad.sh file.

note: user with ARM64 architecture need to manually install the dependencys since /ect/DependencyInstaller.sh file has few packages that are hard coded to point to AMD64 architecture.

## 2. Ibex Design PPA Improvement Updates

To improve the PPA of ibex design following files were updated based on Autotuner feature availabel with ORFS:

a. update /design/asap7/ibex/config.mk as below:

![image](https://user-images.githubusercontent.com/33462440/228996177-022aaa52-bc3b-48fe-907b-b74afc395207.png)

b. updated cts.tcl script to include -repair_tns 100 argument along with reapir_timing command

![image](https://user-images.githubusercontent.com/33462440/228997056-a8c87447-5b8d-4712-8937-33cd5892f192.png)

c. update global_route.tcl to change the global_routing_layer_adjustment to 0.4 from 0.5 for beter global routing results

![image](https://user-images.githubusercontent.com/33462440/229003527-90fc9408-ff8f-439f-8b9e-e9ea7d40f535.png)

d. updated detail_route.tcl in scripts folder to use write_sdc command and repair_timing command

![image](https://user-images.githubusercontent.com/33462440/228997416-68f5cfb1-3fcf-457a-a5b3-a1b7ed044b39.png)

e. updated final_report.tcl to include repair_design and repair_timing command to get clean final design gds

![image](https://user-images.githubusercontent.com/33462440/228998107-8f4b2d58-64ce-4c35-9aeb-7af3157d74c8.png)

f. updated make file to use route.sdc instead of copying cts.sdc to route.sdc

![image](https://user-images.githubusercontent.com/33462440/228998428-64feb181-d1b9-4d9e-9841-dbaa5335a878.png)

# Results
## Before update (reference run):
1. PPA:

![Screenshot 2023-03-30 at 4 48 28 PM](https://user-images.githubusercontent.com/33462440/228998733-fa2578f7-ce10-4489-8bac-5b6ecbbc2d00.png)

2. Runtime:

![image](https://user-images.githubusercontent.com/33462440/228999120-dc7cc334-2284-4778-a879-0e77efa02244.png)

## After Updates:
1. PPA:

![Screenshot 2023-03-30 at 4 49 24 PM](https://user-images.githubusercontent.com/33462440/228999271-e405e030-62bf-405a-80b2-08fedb626cc9.png)

2. Runtime:

![Screenshot 2023-03-30 at 4 41 21 PM](https://user-images.githubusercontent.com/33462440/228999392-c4903a70-f2de-4158-93c6-0fef47feb971.png)


## Conclution:

After the updates are done, the utilization has gone down by 4%, design area was reduced by 8%, power reduce by 23%. however there was slight increase in toltal run time of 8% (254 sec)

# Using the Flow

- See the OpenROAD [documentation here](https://openroad.readthedocs.io/en/latest/).
- How to [start using OpenROAD flow here](https://openroad-flow-scripts.readthedocs.io/en/latest/user/GettingStarted.html).
- Our [user guide here](https://openroad-flow-scripts.readthedocs.io/en/latest/user/UserGuide.html).
- Our [Flow Tutorial here](https://openroad-flow-scripts.readthedocs.io/en/latest/tutorials/FlowTutorial.html).

# Citing this Work

If you use this software in any published work, we would appreciate a citation!
Please use the following references:

```
@article{ajayi2019openroad,
  title={OpenROAD: Toward a Self-Driving, Open-Source Digital Layout Implementation Tool Chain},
  author={Ajayi, T and Blaauw, D and Chan, TB and Cheng, CK and Chhabria, VA and Choo, DK and Coltella, M and Dobre, S and Dreslinski, R and Foga{\c{c}}a, M and others},
  journal={Proc. GOMACTECH},
  pages={1105--1110},
  year={2019}
}
```

A copy of this paper is available
[here](http://people.ece.umn.edu/users/sachin/conf/gomactech19.pdf) (PDF).

```
@inproceedings{ajayi2019toward,
  title={Toward an open-source digital flow: First learnings from the openroad project},
  author={Ajayi, Tutu and Chhabria, Vidya A and Foga{\c{c}}a, Mateus and Hashemi, Soheil and Hosny, Abdelrahman and Kahng, Andrew B and Kim, Minsoo and Lee, Jeongsup and Mallappa, Uday and Neseem, Marina and others},
  booktitle={Proceedings of the 56th Annual Design Automation Conference 2019},
  pages={1--4},
  year={2019}
}
```

A copy of this paper is available
[here](https://vlsicad.ucsd.edu/Publications/Conferences/371/c371.pdf) (PDF).

If you like the tools, please give us a star on our GitHub repos!

## License

The OpenROAD-flow-scripts repository (build and run scripts) has a BSD 3-Clause License.
The flow relies on several tools, platforms and designs that each have their own licenses:

- Find the tool license at: `OpenROAD-flow-scripts/tools/{tool}/` or `OpenROAD-flow-scripts/tools/OpenROAD/src/{tool}/`.
- Find the platform license at: `OpenROAD-flow-scripts/flow/platforms/{platform}/`.
- Find the design license at: `OpenROAD-flow-scripts/flow/designs/src/{design}/`.

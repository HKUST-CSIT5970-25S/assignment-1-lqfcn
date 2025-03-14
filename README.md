[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: LIAO, Qifan
### Student Id: 21079456
### Email: qliaoad@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    Solution:
    Name of measurement tool: Phoronix Test Suite

    > Example config: phoronix-test-suite run pts/compress-7zip

    This parameter "pts/compress-7zip" indicates it measures CPU performance by doing compression tasks.
    
    > Example result: 

                    Test: Compression Rating:
                        3435
                        3463
                        3478

                    Average: 3459 MIPS
                    Deviation: 0.63%

                    Test: Decompression Rating:
                        3055
                        3052
                        3052

                    Average: 3053 MIPS
                    Deviation: 0.06%
    The results above quantifies the CPU's capability of performing compression and decompression tasks. The deviation value indicates the stability of different rounds of tests.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        |      CPU performance      | Memory performance |
    | ----------- | ------------------------- | ------------------ |
    | `t2.micro`  |   3459 MIPS / 3053 MIPS   |    10368.08 MB/s   |
    | `t2.medium` |   9830 MIPS / 5906 MIPS   |    19104.22 MB/s   | 
    | `c5d.large` |   7449 MIPS / 4899 MIPS   |    13388.91 MB/s   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    > t2.micro  has 1 vCPU and 1 GiB of memory;
    > t2.medium has 2 vCPU and 4 GiB of memory;
    > c5d.large has 2 vCPU and 4 GiB of memory;

    Overall, VMs with more vCPU and bigger memory will perform better, but the results won't increase proportionally. 
    
    Also, VMs with the same amount of vCPUs and memory may have very different performance as well.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |      3707      |   0.231  |
    | `m5.large` - `m5.large`   |      5048      |   0.163  |
    | `c5n.large` - `c5n.large` |      5069      |   0.138  |
    | `t3.medium` - `c5n.large` |      2877      |   0.558  |
    | `m5.large` - `c5n.large`  |      2765      |   0.718  |
    | `m5.large` - `t3.medium`  |      4557      |   0.156  |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |      33.2      |   61.938 |
    | N. Virginia - N. Virginia |      5079      |   0.163  |
    | Oregon - Oregon           |      5059      |   0.169  |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

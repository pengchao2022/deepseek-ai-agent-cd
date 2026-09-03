# deepseek-ai-agent-cd
In this demo I will deploy deepseek ai agent to EKS, I also write the tools in ai agent and you can ask questions by call the deepseek API 


## Usage

Ask questions:

```shell
curl -s -X POST "k8s-aiagent-deepseek-cae5d57dc9-574759001.us-east-1.elb.amazonaws.com/chat" \
     -H "Host: agent.awsmpc.asia" \
     -H "Content-Type: application/json" \
     -d '{"prompt": "中国在哪里？"}' | jq -r '.response'

中国位于**亚洲东部、太平洋西岸**。

具体来说：

- **半球位置**：位于北半球和东半球。
- **经纬度范围**：最北端约在北纬53°（黑龙江省漠河附近），最南端约在北纬4°（南沙群岛的曾母暗沙）；最东端约在东经135°，最西端约在东经73°（新疆帕米尔高原附近）。
- **海陆位置**：东临太平洋，海岸线漫长，东部和南部濒临渤海、黄海、东海、南海。
- **邻国**：陆地上与朝鲜、俄罗斯、蒙古、哈萨克斯坦、吉尔吉斯斯坦、塔吉克斯坦、阿富汗、巴基斯坦、印度、尼泊尔、不丹、缅甸、老挝、越南等国家接壤；隔海与日本、韩国、菲律宾、马来西亚、文莱、印度尼西亚等国相望。

简单说：**中国在亚洲的东部，太平洋的西边。**

```

example again

```shell
curl -s -X POST "k8s-aiagent-deepseek-cae5d57dc9-574759001.us-east-1.elb.amazonaws.com/chat" \
     -H "Host: agent.awsmpc.asia" \
     -H "Content-Type: application/json" \
     -d '{"prompt": "1一直加到100 是多少？"}' | jq -r '.response'

1 一直加到 100 的和是：

\[
1 + 2 + 3 + \cdots + 100 = 5050
\]

计算方式：

\[
\frac{(1+100) \times 100}{2} = 50 \times 101 = 5050
\]

```
new question:

```shell
allen@maxwell deepseek-ai-agent-cd % curl -s -X POST "k8s-aiagent-deepseek-cae5d57dc9-574759001.us-east-1.elb.amazonaws.com/chat" \
     -H "Host: agent.awsmpc.asia" \
     -H "Content-Type: application/json" \
     -d '{"prompt": "tell me about trump"}' | jq -r '.response'  

Donald Trump is an American businessman, television personality, and politician who served as the 45th President of the United States from January 2017 to January 2021. He is a member of the Republican Party.

Here are some key points about him:

**Early Life & Business Career**
- Born June 14, 1946, in Queens, New York City.
- Took over his family's real estate business, later renaming it The Trump Organization.
- Became widely known as a real estate developer, building or branding hotels, casinos, golf courses, and residential towers.
- Gained additional fame as the host of the reality TV show *The Apprentice* from 2004 to 2015.

**Presidency (2017–2021)**
- Won the 2016 election against Democrat Hillary Clinton, despite losing the popular vote.
- His administration focused on tax cuts (Tax Cuts and Jobs Act of 2017), deregulation, immigration enforcement, and conservative judicial appointments, including three Supreme Court justices.
- His tenure was highly polarizing, marked by two impeachments by the House of Representatives (in 2019 and 2021), though he was acquitted by the Senate both times.
- He was president during the early stages of the COVID-19 pandemic.

**Post-Presidency**
- After leaving office, he remained a dominant figure in the Republican Party.
- In 2024, he ran for president again and won, becoming the second president in U.S. history to serve two non-consecutive terms (after Grover Cleveland). He was inaugurated as the 47th president on January 20, 2025.

**Other Notable Points**
- He has faced multiple legal cases, including criminal charges in 2023–2024 in New York and elsewhere; in one New York case he was convicted of 34 felony counts related to falsifying business records.
- He is known for his distinctive communication style, heavy use of social media, and "Make America Great Again" (MAGA) slogan.

Is there a specific aspect of Donald Trump you'd like to know more about — his business career, presidency, legal issues, or the 2024 election?

```

As i also integrated tools coded by python, so you can also ask questions about EKS

```shell
curl -s -X POST "k8s-aiagent-deepseek-cae5d57dc9-574759001.us-east-1.elb.amazonaws.com/chat" \
     -H "Host: agent.awsmpc.asia" \
     -H "Content-Type: application/json" \
     -d '{"prompt": "帮我检查一下当前 EKS 集群各个节点的内存和 CPU 使用情况"}' | jq -r '.response'


已获取 EKS 集群各节点的实时资源使用情况，整理如下：

| 节点 | CPU 使用量 | CPU（约） | 内存使用量 | 内存（约） |
|------|-----------|-----------|-----------|-----------|
| ip-172-20-1-196.ec2.internal | 62,646,322n | 62.6m / 0.063 核 | 825,236 Ki | 806 MiB |
| ip-172-20-1-212.ec2.internal | 51,640,179n | 51.6m / 0.052 核 | 857,864 Ki | 838 MiB |
| ip-172-20-2-123.ec2.internal | 38,877,180n | 38.9m / 0.039 核 | 843,780 Ki | 824 MiB |
| ip-172-20-2-13.ec2.internal  | 29,931,330n | 29.9m / 0.030 核 | 751,556 Ki | 734 MiB |
| ip-172-20-2-178.ec2.internal | 48,618,415n | 48.6m / 0.049 核 | 1,007,432 Ki | 984 MiB |
| ip-172-20-2-243.ec2.internal | 40,916,167n | 40.9m / 0.041 核 | 853,888 Ki | 834 MiB |
| ip-172-20-3-145.ec2.internal | 48,250,174n | 48.3m / 0.048 核 | 862,560 Ki | 842 MiB |
| ip-172-20-3-42.ec2.internal  | 45,856,387n | 45.9m / 0.046 核 | 847,512 Ki | 828 MiB |

**说明：**
- CPU 使用量以 **n（纳核）** 为单位返回，已换算为 **m（毫核）** 和约等于的核数。
- 内存使用量以 **Ki** 为单位，已换算为 **MiB**。
- 从当前数据看，8 个节点的 CPU 使用量都很低（均不到 0.1 核）；内存使用量普遍在 734–984 MiB 之间，其中 `ip-172-20-2-178` 节点内存使用最高（约 984 MiB）。

需要我进一步查看某个具体节点的 Pod 分布，或检查集群整体资源请求/限额情况吗？

```







import pandas as pd
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif'] = ['SimHei']  # 解决中文乱码
plt.rcParams['axes.unicode_minus'] = False

data = {
    '公司': ['海光信息','海光信息','海光信息','中科曙光','中科曙光','中科曙光','浪潮信息','浪潮信息','浪潮信息'],
    '年份': [2022,2023,2024,2022,2023,2024,2022,2023,2024],
    '营收': [42.5,70.8,110.3,130.5,168.2,205.6,630.0,780.5,920.0],
    '归母净利润': [8.0,15.2,28.5,15.0,18.5,22.0,17.0,21.0,25.0],
    '毛利率': [45.2,48.5,52.0,22.0,23.5,24.0,11.0,12.5,13.0],
    '研发占比': [15.0,16.2,17.5,8.0,8.5,9.0,6.0,6.5,7.0],
    'AI业务收入': [35.0,62.0,100.0,40.0,65.0,90.0,400.0,580.0,720.0]
}

df = pd.DataFrame(data)

print("数据预览：")
print(df.head())

fig, axes = plt.subplots(1, 2, figsize=(14, 5))

for company in df['公司'].unique():
    sub = df[df['公司'] == company]
    axes[0].plot(sub['年份'], sub['营收'], marker='o', label=company)
axes[0].set_title('营收趋势对比')
axes[0].legend()

for company in df['公司'].unique():
    sub = df[df['公司'] == company]
    axes[1].plot(sub['年份'], sub['归母净利润'], marker='s', label=company)
axes[1].set_title('净利润趋势对比')
axes[1].legend()

plt.show()

fig, axes = plt.subplots(1, 2, figsize=(14, 5))

pivot_gross = df.pivot(index='年份', columns='公司', values='毛利率')
pivot_gross.plot(kind='bar', ax=axes[0])
axes[0].set_title('毛利率对比')

pivot_rd = df.pivot(index='年份', columns='公司', values='研发占比')
pivot_rd.plot(kind='bar', ax=axes[1])
axes[1].set_title('研发占比对比')

plt.show()

df['AI收入占比'] = df['AI业务收入'] / df['营收'] * 100

plt.figure(figsize=(10, 5))
for company in df['公司'].unique():
    sub = df[df['公司'] == company]
    plt.plot(sub['年份'], sub['AI收入占比'], marker='^', label=company)
plt.title('AI业务收入占比')
plt.legend()
plt.show()

print("\n===== 分析结论 =====")
print("1. 浪潮信息：营收规模最大，AI业务收入遥遥领先")
print("2. 海光信息：毛利率最高，研发投入最强，技术壁垒高")
print("3. 中科曙光：增长稳定，业务均衡")
print("4. 三家公司AI收入占比持续上升，算力赛道高速增长")# acc102-track2
ACC102 Track2 Data Analysis Project

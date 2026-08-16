# 玩娃日记 · SuJiu 的娃柜工作台

BJD 娃娃 + 毛娘业务个人管理工作台（单文件 HTML，无任何外部依赖）。

## 在线使用

由 **GitHub Pages** 永久托管，手机/电脑均可打开：

> **https://sujiu489.github.io/wanwa-riji/**

## 功能

- 👗 衣服管理（分类橱窗 / 陈列、筛选、图片上传）
- 📏 体子管理与尺寸对比
- 📅 日历与想买清单
- 📝 记事本（富文本便签）
- 💗 毛娘业务（工具 / 库存 / 收入 / 单主）
- ⚙️ 设置：导出 / 导入 JSON 备份
- 💾 自动保存：每次修改立即写入本机（localStorage + IndexedDB 双层），打开自动恢复
- ☁️ 云同步（Supabase，可选）：点击侧边栏 ☁ 胶囊即可连接 / 立即同步，多设备数据一致

## 云同步接入（首次 3 步）

1. 在 [supabase.com](https://supabase.com) 免费建项目，SQL Editor 执行（应用设置页有同款可复制）：

```sql
create table if not exists cabinet_data (
  room text primary key,
  data jsonb not null,
  updated_at timestamptz not null default now()
);
alter table cabinet_data enable row level security;
create policy "sync_all" on cabinet_data for all using (true) with check (true);
```

2. 项目设置 → API，复制 Project URL 和 anon key
3. 打开工作台 → 点击左侧 ☁ 胶囊 → 填入 URL / 公钥 / 同步码 → 连接云端

多台设备填**同一个同步码**即可互相同步。

## 数据与隐私

- 数据默认只保存在你自己设备的浏览器本地，任何人打开链接都看不到你的数据
- 连接云同步后数据存放在你自己的 Supabase 账号
- 建议定期在「设置 → 导出全部数据备份」留底

## 更新部署

`index.html` 即完整应用，修改后 push 到 main 分支，Pages 自动更新。

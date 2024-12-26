# 打包一个自己的React组件库
>参考：[React 编写私有 UI 组件库（上）之组件库发布完整流程 - 稀土掘金](https://juejin.cn/post/6905661755150565384)

基于Storybook。
## 项目搭建
```powershell
pnpm create vite
cd pixely-ui
pnpm dlx storybook@latest init
```
## 编写故事
>参考：[如何编写故事 - Storybook 中文](https://storybook.org.cn/docs/writing-stories)

Storybook将组件以`故事`的形式保存。在故事中，组件的对象和props在`Meta`中被声明，同时还可以通过`StoryObj<T>`声明组件的各种示例用法。
```tsx
// Avatar.stories.tsx
import type { Meta, StoryObj } from '@storybook/react'

import Avatar from './Avatar'
import avatar from '../../../assets/avatar.jpg'

const meta: Meta<typeof Avatar> = {
    component: Avatar
}

export default meta

type Story = StoryObj<typeof Avatar>;
 
export const Primary: Story = {
  args: {
    src: avatar
  },
}
```
以上是一个Storybook故事。Storybook将会自动识别这些故事并将其呈现在网页上。
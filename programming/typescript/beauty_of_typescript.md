# TypeScript魅力时刻
### 懒加载SVGR组件的类型声明
SVGR是一个可用于各种前端打包工具链的，用于方便在React中直接将svg图像文件导入为React组件的工具库。

React.lazy()函数可以实现组件的“懒加载”——换句话说，按需加载，而不是同首屏一起加载。

以下是React懒加载SVGR组件的类型声明，如果你需要的话。
```typescript
type LazySvgr = LazyExoticComponent<ComponentType<FC<SVGProps<SVGElement>>>>
```
太美丽了尖括号。

---
### 使你的组件属性继承DOM Attributes
>- [React Batter Wrapper Component (ComponentPropsWithoutRef) | by WeiYun | Medium](https://medium.com/@weiyun0912/react-batter-wrapper-component-componentpropswithoutref-de6b0991adce)
>- [Useful Patterns by Use Case | React TypeScript Cheatsheets](https://react-typescript-cheatsheet.netlify.app/docs/advanced/patterns_by_usecase/#wrappingmirroring-a-html-element)

React团队当然考虑到这种需求了，所以：
```typescript
interface RandomComponentProps extends ComponentPropsWithoutRef<'div'> {
    // 你的组件自定义属性，注意不要与DOM Attributes重名...
    randomProp: any
}
```
当然，如果你要继承其他标签的DOM Attributes，只需要替换`ComponentPropsWithoutRef<T>`中的泛型参数就可以了，比如`ComponentPropsWithoutRef<'button'>`就代表`<button />`标签的DOM Attributes。

如果你真的打算这么写，你会和ES6的对象解构语法成为好朋友的。
```tsx
const RandomComponent: React.FC<RandomComponentProps> = ({
    randomProp = 'LOL',
    ...divAttributes
}: RandomComponentProps) => {
    return (
        <div {...divAttributes}>
            {randomProp}
            {/** 你乱七八糟的JSX */}
        </div>
    )
}
```
你还可以用`ComponentPropsWithoutRef<T>`继承任意自定义组件的属性类型：
```tsx
interface WrappedComponentProps = ComponentPropsWithoutRef<typeof RandomComponent>;
```
还有，对的，还有`ComponentProps<T>`和`ComponentPropsWithRef<T>`。它们的用法都相同，唯一区别是只有`ComponentPropsWithoutRef<T>`会遮盖掉`ref`，除此之外命名上的差异主要用于提供上下文信息（告诉代码阅读者这个组件会不会对外暴露`ref`）。

还有，继承DOM Attributes不只有这些方法，只不过这些方法实践起来是最好的。详见参考网址中的第二个。

不觉得这很酷吗，很符合我对TypeScript的想象。
This is a hot take. I'm not really understand the meaning of any UI library, something like MUI. This is especially true when I see most of the components are just combinations of simpliest styles and HTMLs without abstracting any useful logic, even the ones who do have logic are just craps with patterns unrecommended by React like `cloneElement()`. Things get even more messier since there aren't really a guideline for React devs to follow for how to build and abstruct things (It's just JavaScript bro), causing hundreds of weird (or ridicilous) implementations to a same feature or function and countless of meanless document texts.

But for my own project, I want best consistency and maintainability for my UI, so certainly I need to bake my own UI library for that. This drags all the problems mentioned above to the surface. To prevent things getting too dumb I need some sort of ground rule.

First, no hidden dataflow. No HOCs that secretly add props to its childs. This is also recommended by React official doc.

## Post Script
I found that the biggest problem when designing APIs is that because I don't have any team numbers (for now), it's hard to catch design flaws since I know all the behind-the-scene details of all the APIs and it makes me easy to avoid pitfalls.
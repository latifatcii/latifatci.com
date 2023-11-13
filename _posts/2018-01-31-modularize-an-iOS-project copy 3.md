---
layout: post
title: Modularize an iOS Project and Add Module Based Executable Apps
---

A **monolith** project is the starter solution when building a new project. Mostly we won't need anything else when we have small-sized projects. But every time, adding a new feature to the codebase increases complexity and build time.

**What we cover in this article:**

- When modularization is necessary

- What the benefits of the modular projects are

- How to modularize a project

- How we can create feature/module-based executable apps.

Imagine you have a simple movie app, and it only has a home page that shows movie names and pictures. It would be overkill to modularize this project, right? But what if you start to add new features like search, movie detail, favorite movies, etc. You will begin to see some difficulties. 

- Build time increases

- Building/running the whole app even if you change small code blocks in a particular feature\file.

- Testing the whole app when you add new unit tests, etc.

**With modularizing the project:**

- **Build** the module only that you have changed. And this can save you from building the whole project, losing time. 

- **Run** tests in every module separately, not the whole project.

- **Reuse** code everywhere.

Also, modularization **separates** responsibilities. When your team grows, everyone can work on a specific module\feature without depending on others and knowing their responsibilities.

**Let's see how to turn a monolith project into a modularized project.**

- Assume we have a folder structure like down below.

![1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643546748156/AOpN_mqMt.png)

As you can see, we should separate responsibilities/logic to modularize your project.

### 1. Creating Workspace
- xcodeproj is not suitable for modular projects. You can only have one module in it. That's why we should create a Workspace.
In the main project, with File -> Save As Workspace, Xcode creates us a workspace.

![9.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643597277472/eYx6_-oph.png)

After saving it in the project folder, you can see the xcworkspace. We will work with this from now.

![10.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643597288263/ycQAwlITy.png)

Now we can start creating modules.

### 2. File -> New -> Project -> Framework

![2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643550005517/Zr9m0wxd7.png)

After choosing a framework, we should type the framework's name like HomeModule, Search Module, etc.

### 3. Choose the main app (its MovieApp in our case) in "Add to" and "Group".

![3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643550223025/KcHUoZTN9.png)

### 4. Changing folder structure

After doing these for all modules we want to create, we will have three projects other than the main app. We can move them to the Modules folder. Then we will have a structure like down below. 

![5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643568286768/o2lOdDNCc.png)

### 5. Move logics to modules
Now, we can move our logic to corresponding modules.  <br /> 
The most important thing that we should be careful of is **decoupling** the modules. Modules shouldn't depend\need each other most of the time. 

**Circular Dependency** is one of the main problems in a modular project that we should avoid.

> In software engineering, a circular dependency is a relation between two or more modules which either directly or indirectly depend on each other to function properly.

- If HomeModule has SearchModule as a dependency, SearchModule should not depend on HomeModule. If there are common things that some of the modules need, we should move them to separate modules like Commons, Kits, Core, etc.

### 6. Add each module to the main app target as a dependency.

![main app.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643597886355/HMvw7Dmzz.png)

Now we can run our modularized app, and its following problems turn:  <br /> 
Why do we have to run the whole app even for minor changes in particular modules? Cant we only run the module and see the differences? **Yes**, we can. 

### 7. File -> New -> Project -> App

![6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643572435520/WS15ZAj2W.png)

We will create a new app just like creating a new project.

### 8. Add corresponding modules to app target as a dependency.

![homeapp.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643595879133/mPvzlDHwc.png)
 
### 9. Navigate to the corresponding module
Navigate to HomeModule in HomeApp instead of starting from the Main.storyboard in HomeApp from AppDelegate.

![8.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643596066459/IbHOO05wO.png)

- Sometimes, you may need some data while navigating to a module. In the main app, you will pass to the next module from the previous module, but when you create a feature-based app, you should mock it and inject it as you see above.

### In the end, our project structure and schemes will look like this.

![folders.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643596583533/_dwO36epe.png)
 
![scheme.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643596587950/GuMrO8B81.png)

![simulator.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643596594701/qUSv8LEIX.png)

### Conclusion

- Monolith projects are enough for **simple** projects.

- The more **extensive** and the more **complex** the project becomes, the more **issues** we will have.

- Modularizing the project mainly saves our **time** and separates **responsibilities/logic**.

- Be careful about **Circular Dependency**.

- Each screen/feature can have its **executable** app.

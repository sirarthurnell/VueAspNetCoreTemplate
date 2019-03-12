# Vue + ASP&#46;NET Core 2.2 Template

Template to start developing with Vue + ASP&#46;NET Core 2.2. It uses TypeScript as scripting language and SCSS as style language. Contains *router* but nothing more, so you can add the things you need instead of removing those you don't need.

I decided to create this template because there are some unsolved problems that make it painful to start a new project with Vue and ASP&#46;NET Core.

Concretely, if you use Razor Pages in your new project, you will find some weird compilation errors about a duplicated attributes:

> ```text
> error CS0579: Duplicate ‘System.Reflection.AssemblyCompanyAttribute’ attribute
> error CS0579: Duplicate ‘System.Reflection.AssemblyConfigurationAttribute’ attribute
> error CS0579: Duplicate ‘System.Reflection.AssemblyFileVersionAttribute’ attribute
> error CS0579: Duplicate ‘System.Reflection.AssemblyInformationalVersionAttribute’ attribute
> error CS0579: Duplicate ‘System.Reflection.AssemblyProductAttribute’ attribute
> error CS0579: Duplicate ‘System.Reflection.AssemblyTitleAttribute’ attribute
> error CS0579: Duplicate ‘System.Reflection.AssemblyVersionAttribute’ attribute
> ```

That issue is solved if you add `<GenerateAssemblyInfo>false</GenerateAssemblyInfo>` to your project file (which is already added to the project file of this template). More details [here](https://jonboulineau.me/blog/dotnet/core-CS0579-error).

There's another problem with the `experimentalDecorators` param of the `tsconfig.json` file. The way to make it work is putting another `tsconfig.json` file at the directory that contains the directory of the ASP&#46;NET Core project (usually next to the solution file, more details [here](https://github.com/vuejs/vetur/issues/815)). The content of the file should be:

```json
{
  "extends": "./PresentationLayer/Client/tsconfig.json"
}
```
I have added some rules to the `tslint.json` file, because the TS linter came almost without any configuration and that makes de development quite annoying.

And another problem I have found and that's pretty annoying is the issue with single quotes and Prettier. Vetur isn't very good at reading Prettier's configurations, so it replaces single quotes with double quotes every time you press `Shift + Alt + F` even if you told Prettier to use single quotes only (more details [here](https://github.com/vuejs/vetur/issues/986)). Another pretty annoying issue that remains unsolved. The solution that always work is adding a `.prettierrc.js` file to the `src` directory with the content:

```javascript
module.exports = {
  singleQuote: true
};
```

That file is added to this template too.

## How to use it

Simply `clone` it and rename those parts you want to rename. Take into account that `tsconfig.json` next to the solution file pointing to the other `tsconfig.json` inside the `Client` directory.

If you don't want to rename it manually, I suggest you using this [tool](https://github.com/sirarthurnell/Renamer) I wrote some time ago. It can make things easier for you.

I hope this template can save you some time next time you want to start a new Vue + ASP&#46;NET Core project.

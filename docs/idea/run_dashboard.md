- Run Dashboard
> 运行指示板

- 作用
> IDEA 中 Dashboard界面化窗口使用，方便管理多应用

- 开始方式
> 打开.idea文件夹下workspace.xml 在project标签内添加以下内容
```xml
<component name="RunDashboard">
    <option name="configurationTypes">
      <set>
        <option value="SpringBootApplicationConfigurationType" />
      </set>
    </option>
</component>
```
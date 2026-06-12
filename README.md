# 在Github Actions上使用`Win_ISO_Patching_Scripts`自动集成`Windows 10`更新

## 说明
1. 本项目的主要目的是：使用`Win_ISO_Patching_Scripts`自动集成`Windows 10/11`更新(使用`Github Actions`自动构建)

## 链接
1. `Windows 10专业版母盘`地址: https://github.com/993671009/UpdateWinISO/releases/tag/Windows10
2. `Win_ISO_Patching_Scripts`地址: https://github.com/adavak/Win_ISO_Patching_Scripts
3. `W10UI`地址: https://github.com/abbodi1406/BatUtil

## 关于`W10UI.ini`
- 本仓库默认使用`Win_ISO_Patching_Scripts`的**预设**`W10UI.ini`
- 若要修改预设，可在本仓库修改`myini\W10UI.ini`，并在相应`yml`文件上将
  `:: copy D:\a\UpdateWinISO\UpdateWinISO\myini\W10UI.ini D:\a\UpdateWinISO\Win_ISO_Patching_Scripts\W10UI.ini /Y`
  改为
  `copy D:\a\UpdateWinISO\UpdateWinISO\myini\W10UI.ini D:\a\UpdateWinISO\Win_ISO_Patching_Scripts\W10UI.ini /Y`

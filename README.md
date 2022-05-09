# Sun-Weather
## Sun Weather是什么？

~~是歌姬吧~~ Sun Weather是一个基于C#编写的，由微软大大提供的WinUI3编写的一款天气软件

~~全靠WE完成~~靠我和we共同完成

## 进度？

1. - [x] 自动定位
2. - [x] UI
3. - [x] 查天气
4. - [x] 日落日出
5. - [x] 感觉像和风速
6. - [ ] 更多功能敬请期待…… 

## 开发团队人名单

BilShiziheng(我) ~~督促~~
WindowsExplorer 开发者 ~~整天骂街~~

## 目前版本？
已经到Release 1.0了，感谢WE的大力支持（

## 部分代码
以下是部分代码qwq
```
        {
            // 初始化窗口
            this.InitializeComponent();
            SearchPage.mainWindow = this;
            this.SetIcon("Assets/App_Icon_Content_64.ico");
            this.SearchLocationAutoSuggestBox.ItemsSource = locationName;
            Configs.LoadConfig();
            //DPIAdapted();
        }

        private ICommand OpenSettingPageCommand
        {
            get
            {
                return new ICommandBase
                {
                    CommandAction = () =>
                    {
                        PageContentFrame.Navigate(typeof(SettingPage));
                        MainNavigationView.IsPaneOpen = false;
                    }
                };
            }
        }

        private async Task<bool> CheckApiKeyAsync(bool showDialog = true)
        {
            async Task ShowContentDialogAsync(string errorCode)
            {
                if (showDialog)
                {
                    ContentDialog contentDialog = new ContentDialog
                    {
                        Title = "提示",
                        Content = $@"请到设置页面配置正确的 API 密钥。
错误代码：{errorCode}",
                        PrimaryButtonText = "去配置",
                        PrimaryButtonCommand = OpenSettingPageCommand,
                        CloseButtonText = "OK",
                        DefaultButton = ContentDialogButton.Primary,
                        XamlRoot = this.Content.XamlRoot
                    };
                    await contentDialog.ShowAsync();
                }
            }
            if (string.IsNullOrEmpty(Configs.ApiKey))
            {
                await ShowContentDialogAsync("400");
                return false;
            }
            try
            {
                await QWeatherAPI.GeoAPI.GetGeoAsync("北京", Configs.ApiKey);
            }
            catch (ArgumentException ex)
            {
                await ShowContentDialogAsync(ex.Message);
                return false;
            }
            return true;
        }
```
## 来自BilShiziheng的留言

hi，这里是开发团队的~~督促的~~石头，这里面的UI是我设计的，~~当然逼着WE换天气图标也是我~~，要是我不告诉你们卡片用了灰色~~其实我告诉we要亚克力，但是他说亚克力有点耗资源~~

以后我们会用力的~~咕咕咕~~开发的，谢谢大家

##下载地址
那你说了这么半天废话？下载地址？
[点这里下载]https://github.com/WinExp/SunWeather/releases/tag/1.0.0

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
private async Task QueryLocationWithAutoSuggestBoxAsync(AutoSuggestBox sender)
{
    try
    {
        if (locationDictionary.ContainsKey(sender.Text))
        {
            return;
        }
        locationDictionary.Clear();
        locationName.Clear();
        if (sender.Text == String.Empty
            || !await CheckApiKeyAsync(false))
        {
            return;
        }
        string cutLocation = sender.Text.Trim().Replace(" ", null);
        string[] replaceString = { "，", "。", "." };
        foreach (string replaceItem in replaceString)
        {
            cutLocation.Replace(replaceItem, ",");
        }
        string[] queryLocation = cutLocation.Split(',');
        GeoResult result;
        if (queryLocation.Length == 1)
        {
            result = await QWeatherAPI.GeoAPI.GetGeoAsync(queryLocation[queryLocation.Length - 1], Configs.ApiKey, limit: 20);
        }
        else
        {
            result = await QWeatherAPI.GeoAPI.GetGeoAsync(queryLocation[queryLocation.Length - 1], Configs.ApiKey, adm: queryLocation[queryLocation.Length - 2], limit: 20);
        }
        foreach (Location location in result.Locations)
        {
            string locationName = location.Name;
            if (!(location.Adm2.Substring(0, location.Name.Length >= location.Adm2.Length ?
                location.Adm2.Length : location.Name.Length) == location.Name))
            {
                locationName = locationName.Insert(0, location.Adm2 + ", ");
            }
            else if (!(location.Adm1.Substring(0, location.Name.Length >= location.Adm1.Length ?
                location.Adm1.Length : location.Name.Length) == location.Name))
            {
                locationName = locationName.Insert(0, location.Adm1 + ", ");
            }
            else
            {
                locationName = locationName.Insert(0, location.Country + ", ");
            }
            locationDictionary.Add(locationName, location);
            this.locationName.Add(locationName);
        }
    }
    catch (ArgumentException ex)
    {
        switch (ex.Message)
        {
            case "404":
                locationName.Clear();
                break;
        }
    }
}
```
## 来自BilShiziheng的留言

hi，这里是开发团队的~~督促的~~石头，这里面的UI是我设计的，~~当然逼着WE换天气图标也是我~~，要是我不告诉你们卡片用了灰色~~其实我告诉we要亚克力，但是他说亚克力有点耗资源~~

以后我们会用力的~~咕咕咕~~开发的，谢谢大家

##下载地址
那你说了这么半天废话？下载地址？
[点这里下载](https://github.com/WinExp/SunWeather/releases/tag/1.0.0 "Sun Weather 最新版下载")

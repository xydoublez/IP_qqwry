# IP_qqwry 纯真IP数据库操作

[![NuGet](https://img.shields.io/nuget/v/QQWry.svg?style=flat)](https://www.nuget.org/packages/QQWry)
[![NuGet](https://img.shields.io/nuget/v/QQWry.DependencyInjection.svg?style=flat)](https://www.nuget.org/packages/QQWry.DependencyInjection)

支持在线更新数据库

## QQWry

    var config = new QQWryOptions()
    {
        DbPath = MapRootPath("~/IP/qqwry.dat")
    };

    var ipSearch = new QQWryIpSearch(config);

    foreach (var ip in preSearchIpArray)
    {
        var ipLocation = ipSearch.GetIpLocation(ip);
        Write(ipLocation);
    }
    Console.WriteLine("记录总数" + ipSearch.IpCount);
    Console.WriteLine("版本" + ipSearch.Version);

## QQWry.DependencyInjection

    var service = new ServiceCollection();

    service.AddQQWry(config);

    var serviceProvider = service.BuildServiceProvider();

    using (var scope = serviceProvider.CreateScope())
    {
        var ipSearchInterface = scope.ServiceProvider.GetRequiredService<IIpSearch>();
        foreach (var ip in preSearchIpArray)
        {
            var ipLocation = ipSearchInterface.GetIpLocation(ip);
            Write(ipLocation);
        }
        Console.WriteLine("记录总数" + ipSearchInterface.IpCount);
        Console.WriteLine("版本" + ipSearchInterface.Version);
    }

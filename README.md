riak.driver.net
===============

Riak.Driver.Net

```csharp
 static void Main(string[] args)
  {
      System.Threading.ThreadPool.SetMinThreads(30, 30);
      Sodao.FastSocket.SocketBase.Log.Trace.EnableConsole();

      var riakClient = Riak.Driver.RiakClientPool.Get("riak.config", "riak1");

      riakClient.Put(new Riak.Driver.RiakObject("bucket1", "key1", "value1"), options => options.SetW(1).SetReturnBody(true)).ContinueWith(c =>
      {
          if (c.IsFaulted) Console.WriteLine(c.Exception.ToString());
          else Console.WriteLine(c.Result.Value.GetString());
      });

      riakClient.Get("bucket1", new string[] { "key1", "key2" }, options => options.SetR(1)).ContinueWith(c =>
      {
          if (c.IsFaulted) Console.WriteLine(c.Exception.ToString());
          else Console.WriteLine(c.Result.Length);
      });
      Console.ReadLine();
  }
  ```

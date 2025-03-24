echo -n "Please enter your name: "
    read name
    echo "Hello, $name!"

Reading user input

    echo -n "Please enter your name: "
    read name
    echo "Hello, $name!"

``` nowrap
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

    echo -n "Please enter your name: "
    read name
    echo "Hello, $name!"

``` highlight
5.times do
  print "Odelay!"
end
```

Odelay!

``` highlight
5.times do
  print "Odelay!"
end
```

``` highlight
5.times do
  print "Odelay!"
end
```

``` highlight
public class ApplicationConfigurationProvider extends HttpConfigurationProvider {

   public Configuration getConfiguration(ServletContext context) {
      return ConfigurationBuilder.begin()
               .addRule()
               .when(Direction.isInbound().and(Path.matches("/{path}")))
               .perform(Log.message(Level.INFO, "Client requested path: {path}"))
               .where("path").matches(".*");
   }
}
```
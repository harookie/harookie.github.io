```python
# src/main/main.py
import sys
import importlib

from configuration import Configuration


def main():
    print(Configuration.var01)
    print(Configuration.var02)


if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit(1)

    profile = sys.argv[1]

    configuration_module = importlib.import_module("configuration.%s" % profile)
    Configuration = eval("configuration_module.Configuration")
    main()
```

```python
# src/configuration/__init__.py
class Configuration:
    var01 = None
    var02 = None
```

```python
# src/configuration/dev.py
from configuration import Configuration as SuperConfiguration


class Configuration(SuperConfiguration):
    var01 = "dev"
```
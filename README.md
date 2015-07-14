# AutoParse

[![auto-parse](art/auto-parse.png)](art/auto-parse.png)

Easy to use ParseObject

before:

```java
ParseObject gameScore = new ParseObject("GameScore");
gameScore.put("score", 1337);
gameScore.put("playerName", "Sean Plott");
gameScore.put("cheatMode", false);
gameScore.saveInBackground();
```

after:

```java
ParseGameScore gameScore = ParseGameScore.create();
gameScore.setScore(1337);
gameScore.setPlayerName("Sean Plott");
gameScore.setCheatMode(false);
ParseGameScore.commit().saveInBackground();
```

```java
ParseQuery<AutoParse_ParseGameScore> = ParseQuery.getQuery(AutoParse_ParseGameScore.class);
// ...
ParseGameScore gameScore = (ParseGameScore) query.findFirst();
gameScore.getScore();
gameScore.getPlayerName();
gameScore.getCheatMode();
```

## Usage


```java
@ParseClassName("GameScore")
@AutoParse
public abstract class ParseGameScore extends ParseObject implements Parcelable {

  public abstract String playerName(); // getString("playerName");
  public String playerName;            // put("playerName", name);

  public abstract Integer score();
  public Integer score;

  public abstract Boolean cheatMode();
  public Boolean cheatMode; 

  public ParseGameScore commit() { // dont be abstract method
      return this;
  }

  public static ParseGameScore create() {
    return new AutoParse_ParseGameScore();
  }
}
```

## Installation

via jitpack(in progress):

```gradle
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.neenbedankt.gradle.plugins:android-apt:1.4'
    }
}

repositories {
    maven { url "https://jitpack.io" }
}

apply plugin: 'android-apt'

dependencies {
    compile 'com.github.8tory.auto-parse:auto-parse:-SNAPSHOT'
    apt 'com.github.8tory.auto-parse:auto-parse-processor:-SNAPSHOT'
}
```

via jcenter(in progress):

```gradle
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.neenbedankt.gradle.plugins:android-apt:1.4'
    }
}

repositories {
    jcenter()
}

apply plugin: 'android-apt'

dependencies {
    compile 'com.infstory:auto-parse:1.0.0'
    apt 'com.infstory:auto-parse-processor:1.0.0'
}
```

## See Also

auto-parse uses compile-time annotation that's faster than runtime annotation reflection.

* https://github.com/8tory/simple-parse via runtime annotation reflection, slower.

## License

```
Copyright 2015 8tory, Inc.
Copyright 2014 Frankie Sardo
Copyright 2013 Google, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

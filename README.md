# less-faster

Because lesscss-maven-plugin is slow as hell.


## Installation

First, take the compileLess file and put it in `/usr/local/bin`. Then make sure you have [lessc](http://lesscss.org/) and the [less-plugin-clean-css](https://github.com/less/less-plugin-clean-css) module installed.

Then put this in your pom.xml. Make sure that your target directory is accurate!

```xml
<profile>
    <id>less-release</id>
    <build>
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>1.4.0</version>
                <executions>
                    <execution>
                        <phase>compile</phase>
                        <goals>
                            <goal>exec</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <executable>compileLess</executable>
                    <arguments>
                        <argument>${project.basedir}</argument>
                        <argument>${project.build.directory}/${project.artifactId}-${project.version}</argument>
                    </arguments>
                </configuration>
            </plugin>
        </plugins>
    </build>
</profile>
```


## What does this do, anyways?

It's pretty short, so take a look! But mostly it runs lessc (which is faster than whatever plugin you're probably using) and will run the compiler on every file in parallel. For my purposes, I was able to lower my speed for 62 files from about 90s every compile cycle to about 10s.

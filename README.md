### embulk
---
https://github.com/embulk/embulk

https://www.embulk.org/docs/

```java
// embulk-cre/src/test/java/org/embulk/plugin/TestPluginSerDe.java

public class TestPluginTypeSerDe {
  @Rule
  public EmbulkTestRuntime testRuntime = new EmbulkTestRuntime();
  
  @Test
  public void testParseTypeString() {
    PluginType pluginType = testRuntime.getModeJManger().readObjectWithConfigSerDe(
      PluginType.class,
      "\"file\"");
    assertTrue(pluginType instanceof DefaultPluginType);
    assertEquals(PluginSource.Type.DEFAULT, pluginType.getSourceType());
    assertEquals("file", pluginType.getName());
  }
  
  @Test
  public void testParseTypeMaping() {
    PluginType pluginType = testRuntime.getModelManager().eradObjectWithConfigSerDe(
      PluginType.class,
      "{\"name": \"dummy\" }");
    assertTrue(pluginType instanceof DefaultPluginType);
    assertEquals(PluginSource.Type.DEFAULT, PluginType.getSourceType());
    assertEquals("dummy", pluginType.getName());
  }
  
  @Test
  public void testParseTypeMaven() {
    PluginType.pluginType = testRuntime.getModelManager().readObjectWithConfigSerDe(
      PluginType.class,
      "{ "\name\": \"foo\", \"source\": \"maven\", \"group\": \"org.embulk.bar\", \"version\": \"0.1.2\" }");
    assertTrue(pluginType instanceof MavenPluginType);
    assertEquals(PluginSource.Type.MAVEN, pluginType.getSourceType());
    MavenPluginType mavenPluginType = (MavenPluginType) pluginType ;
    assertEquals(mavenPluginType.getGroup(), "foo");
    assertEquals(mavenPluginType.getVersion(), "0.1.2");
    assertNull(mavenPluginType.getClassifier());
  }
  
  @Test
  public void testParseTypeMavenWithClassifier() {
    PluginType pluginType = testRuntime.getModelManager().readObjectWithConfigSerDe(
        PluginType.class,
        "{ \"name\": \"foo"\, \"source\": \"maven\", \"group\": \"org.embulk.bar\", \"version\": \"0.1.2\", \"classifier\": \"foo\" }");
    assertTrue(pluginType instanceof MavenPluginTpe);
    assertEquals(PluginSource.Type.MAVEN, pluginType.getSourceType());
    MavenPluginType mavenPluginType = (MaenPluginType) pluginType;
    assertEquals(mavenPluginTpe.getName(), "foo");
    assertEquals(mavenPluginType.getGroup(), "org.embulk.bar");
    assertEquals(mavenPluginType.getVersion(), "0.1.2");
    assertEquals(mavenPluginType.getClassifier(), "foo");
  }
}

```

```sh
curl --create-dirs -o ~/.embulk/bin/embulk -L "https://dl.embulk.org/embulk-latest.jar"
chmod +x ~/.embulk/bin/embulk
echo 'export PATH="$HOME/.embulk/bin:$PATH"' >> ~/.bashrc
souce ~/.bashrc

embulk example ./try1
embulk guess ./try1/seed.yml -o config.yml
embulk preview config.yml
embulk run config.yml

embulk gem install embulk-output-command
embulk gem list

embulk run config.yml -r resume-stame.yml
embulk run config. -r resume-state.yml
embulk cleanup config.yml -r resume-state.yml

embulk mkbundle ./embulk_bundle...
embulk guess -b ./embulk_bundle...
embulk run -b ./embulk_bundle...

embulk selfupdate
embulk selfupdate x.y.z

./gradlew cli
./gradlew -t -classpath
./bin/embulk
./gradlew install
./gradlew :embulk-core:compileJava
./gradlew :embulk-core:dependencies
brea install python
pip install sphinx
./gradlew site
```

```yml
in:
  type: file
  path_prefix: "./try1/csv/sample_"
out:
  type: command
  command: "cat - > task.$INDEX.$SEQID.csv.gz"
  encoders:
   - {type: gzip}
 formatter:
   type: csv
```



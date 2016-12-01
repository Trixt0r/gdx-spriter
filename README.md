# LibGDX Spriter

This project implements the abstract loader and drawer classes of the generic
Java implementation for Spriter.

Simply import `com.brashmonkey.spriter.gdx.Loader` and
`com.brashmonkey.spriter.gdx.Drawer` and you should be ready to go.

Example
=======

```
public class SpriterTest implements ApplicationListener {

	Player player;
	ShapeRenderer renderer;
	SpriteBatch batch;
	Drawer drawer;
	Loader loader;
	OrthographicCamera cam;

	@Override
	public void create() {
		cam = new OrthographicCamera();
		cam.zoom = 1f;
		renderer = new ShapeRenderer();
		batch = new SpriteBatch();
		FileHandle handle = Gdx.files.internal("assets/monster/basic_002.scml");
		Data data = new SCMLReader(handle.read()).getData();

		loader = new Loader(data);
		loader.load(handle.file());

		drawer = new Drawer(loader, batch, renderer);

		player = new Player(data.getEntity(0));
	}

	@Override
	public void resize(int width, int height) {
		cam.setToOrtho(false, Gdx.graphics.getWidth(), Gdx.graphics.getHeight());
		cam.position.set(0, 0, 0f);
		cam.update();
		renderer.setProjectionMatrix(cam.combined);
		batch.setProjectionMatrix(cam.combined);
	}

	@Override
	public void render() {
		Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT);

		player.update();

		batch.begin();
			drawer.draw(player);
		batch.end();

	}

	@Override
	public void pause() {
	}

	@Override
	public void resume() {
	}

	@Override
	public void dispose() {
		renderer.dispose();
		loader.dispose();
	}
}
```

For more examples, checkout the
[examples](https://github.com/Trixt0r/spriter-examples) based on LibGDX.

Dependency management with maven
================================
Add the following repository url:

```
https://raw.github.com/Trixt0r/gdx-spriter/mvn/
```
GroupId is `com.brashmonkey.spriter`

ArtifactId is `gdx-spriter`
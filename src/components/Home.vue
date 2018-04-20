<template>
  <div >
    <h1>Soccer</h1>
    <div id="engine"></div>
    <div id="ball" ></div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      msg: 'Emoji Soccer',
    };
  },
  mounted() {
    /* eslint-disable */
    var Engine = Matter.Engine,
        Render = Matter.Render,
        Runner = Matter.Runner,
        MouseConstraint = Matter.MouseConstraint,
        Mouse = Matter.Mouse,
        World = Matter.World,
        Bodies = Matter.Bodies;

    // create engine
    var engine = Engine.create(),
        world = engine.world;

    engine.world.gravity.x = 0;
    engine.world.gravity.y = 0;
  
    // create renderer
    var render = Render.create({
        element: document.body,
        engine: engine,
        options: {
            width: 800,
            height: 600,
            showAngleIndicator: true,
            showCollisions: true,
            showVelocity: true
        }
    });

    Render.run(render);

    // create runner
    var runner = Runner.create();
    Runner.run(runner, engine);

    // add bodies
    var rest = 0.9, 
        space = 600 / 5;
    
    World.add(world, [
        Bodies.circle(100 + space * 3, 150, 25, { restitution: rest }),
        // walls
        Bodies.rectangle(400, 0, 800, 10, { isStatic: true }),
        Bodies.rectangle(400, 600, 800, 10, { isStatic: true }),
        Bodies.rectangle(800, 300, 10, 600, { isStatic: true }),
        Bodies.rectangle(0, 300, 10, 600, { isStatic: true })
    ]);

    // add mouse control
    var mouse = Mouse.create(render.canvas),
        mouseConstraint = MouseConstraint.create(engine, {
            mouse: mouse,
            constraint: {
                stiffness: 0.2,
                render: {
                    visible: false
                }
            }
        });

    World.add(world, mouseConstraint);

    // keep the mouse in sync with rendering
    render.mouse = mouse;

    // fit the render viewport to the scene
    Render.lookAt(render, {
        min: { x: 0, y: 0 },
        max: { x: 800, y: 600 }
    });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

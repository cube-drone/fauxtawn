
# Fauxtawn

Pronounced "Photon", fauxtawn is a node wrapper for the Unity Photon Javascript SDK,
which is documented [here](https://doc-api.photonengine.com/en/javascript/current/index.html).

The Unity Photon Javascript SDK expects a WebSocket that works a little bit differently than
node WebSockets, so this has been changed to match. Also, the `__extends` function has been
moved to Photon.extends so that it can be exported with the rest of the code.


### Let's Get Started

Javascript doesn't really support classical inheritance like you would find in C#.

Some people might think of this as an excuse to write the library in a style
idiomatic to the JavaScript language - but not the developers of this library.
Nope, this library is going to do everything it can to pretend to be C#.

So you're going to be implementing your functionality as a subclass of a parent class,
where you override any functions that you need.

Install it with:

    npm install -s fauxtawn

Then use it like this:

    let Photon = require("fauxtawn").Photon;

    let regionMaster = 'US';
    let appId = '3e3ee33e-0999-3eee-e3ee-33333eeeee3e';
    let version = '1.0';
    // If you're using PUN networking, you'll need to include the PUN version with your version.
    // let pun_version = '1.51';
    // version = `${version}_${pun_version}`;

    var DemoLoadBalancing = (function (_super) {
        Photon.extends(DemoLoadBalancing, _super);
        function DemoLoadBalancing() {
            _super.call(this, Photon.ConnectionProtocol.Wss, appId, version);
            console.log(this.logger.format("Init", this.getNameServerAddress(), appId, version));
        }
        DemoLoadBalancing.prototype.start = function () {
            // connect if no fb auth required
            this.connectToRegionMaster(regionMaster);
        };
        DemoLoadBalancing.prototype.onRoomList = function(rooms) {
            console.log(rooms);
            this.disconnect();
        }
        return DemoLoadBalancing;
    }(Photon.LoadBalancing.LoadBalancingClient));

Ta da! A script that allows you to pull a list of rooms out of Photon. Nice.

### I want to do more, different things, though.

That sounds hard! You'd best figure that out on your own! Use the API documentation!

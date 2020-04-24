##React
* Add `react.js` and `react-dom.js` (and `browser.js` from babel-core )
* `JSX` is xml syntax inside of JS
* Rendering sometingh
```javascript
    <script type ="text/babel">
        ReactDOM.render(
            <h1>Hello</h1>,
            document.getElementById("area")
            );

    </script>
```
* Write JS code and expressions inside `{}`
* **Component** (naming should like "CompName")
```javascript
<script type ="text/babel">
    var HelloComp = React.createClass({
        render: function() {
            return (
                <div className="helloComp">
                    <h1>HelloWorld</h1>
                </div>
            );
  }
});

    ReactDOM.render(
        <HelloComp/>,
        document.getElementById("area")
    );
</script>
```
* **Props** stores data (like attributes in html tags)

```javascript
<script type ="text/babel">
    var HelloComp = React.createClass({
        //defines default values of props
        getDefaultProps: function(){
            return {
                name: "There"
            }
        },


        render: function() {
            return (
                <div className="helloComp">
                    <h3>Hello {this.props.name}</h3>
                </div>
            );
  }
});

    ReactDOM.render(
        <div className="container">
            <HelloComp name="Abdullah"/>
            <HelloComp />
        </div>,


        document.getElementById("area")
    );
    </script>
```
* Conditioals

* **States**

```javascript
var HelloComp = React.createClass({
    propTypes:{
        name: React.PropTypes.string
    },


    //defines default values of props
    getDefaultProps: function(){
        return {
            name: "There"
        }
    },

    getInitialState: function() {
        return {
            value: 1

        }
    },

    componentDidMount: function() {
        this.setState({
            value: this.state.value + 15
        });
    },

    changeState: function(){
        this.setState({
            value: this.state.value + 1}
    )},

    render: function() {
        return (
            <div className="helloComp">
                <h3>Hello {this.props.name}</h3>
                <p>
                    State: {this.state.value}
                </p>
                <button onClick= {this.changeState} type="button" name="button">Increase state</button>
            </div>
        );
}
});
```

# Universe Accounts UI

A replacement for `accounts-ui` designed to work in [Universe](http://unicms.io) ecosystem: [Modules](https://atmospherejs.com/universe/modules), React and Semantic UI.

## Installation

    meteor add universe:accounts-ui

- This package assumes that you're using React
- This package uses Semantic UI styling classes, but you have to add styles on your own, e.g.
    * `meteor add semantic:ui`

- Login options will show based on installed packages and you need to add them manually, e.g.
    * `meteor add accounts-password accounts-facebook ...`

## Usage

- You need to set up own routes
- Place `accounts-ui` components where you wish to render forms

Basic usage could look like:

    import {ComboBox} from 'meteor/universe:accounts-ui';

    Router.route('/login', {
        name: 'login',
        action () {
            mount(Layout, {
                content: <ComboBox />
            });
        }
    });

### Available components

- `LoginBox` - simple login form
- `RegisterBox` - simple register form
- `ComboBox` - both above forms combined into one
- `ResetPasswordBox` - password reset form
- `EnrollmentBox` - password init form

## Configuration

No config yet, but will have similar configuration to `accounts-ui`.

## Know issues

- Has UI for password reset, but don't provide server-side functionality yet.
- You need to set ServiceConfiguration options for external services on your own, no forms yet

## Examples

### EnrollmentBox

```javascript
import {EnrollmentBox} from 'meteor/universe:accounts-ui';

Accounts.onEnrollmentLink((token, done) => {
    Meteor.setTimeout(() => { // to mount after FlowRouter (you can also use Accounts.urls.enrollAccount)
        const onComplete = () => {
            done();
            FlowRouter.go('/');
        };
        mount(MainLayout, {
            content: <EnrollmentBox token={token} onComplete={onComplete} />
        });
    }, 100);
});```

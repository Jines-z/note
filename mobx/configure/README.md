## Mobx 4 严格模式
```Javascript
import {observable, action, configure} from 'mobx'
configure({enforceActions:true})
class Store {
    @observable userInfo = {
        name : ''
    }
    @observable loading = false
    @action updateName = (name) => {
        this.userInfo.name = name
    }
    @action updateLoading = (boolean) => {
        this.loading = boolean
    }
}

export default new Store()
```
[目录](https://github.com/jines-z/note)

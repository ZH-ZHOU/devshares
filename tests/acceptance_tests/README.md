# BitShares Acceptance Testing

This repository holds the BitShares acceptance tests implemented on top of Ruby's cucumber framework.


## Installation

**Install Ruby:**

On **Linux** I recommend to use rvm to install Ruby, here is how to do this on Ubuntu:

``` bash
  $ sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev curl
  $ curl -L https://get.rvm.io | bash -s stable
  $ source ~/.rvm/scripts/rvm
  $ echo "source ~/.rvm/scripts/rvm" >> ~/.bashrc
  $ rvm install 2.1.3
  $ rvm use 2.1.3 --default
```

On **OS X** you can install it via brew:
```bash
  $ brew install ruby
```


On **Windows** (not tested) you can use RubyInstaller http://rubyinstaller.org

  
**After you installed Ruby, install bundler gem:**
```bash
  $ gem install bundler
```

Now you can install all dependencies by typing 'bundle' inside acceptance_tests dir.
 
If you are using out of source builds, you need to define BTS_BUILD environment variable pointing to your bitshares build directory, e.g.:
```bash
  $ export BTS_BUILD=/home/user/bitshares/build
```
  
## Usage
  
Run the tests (features) via 'cucumber' command:
```bash
  $ cucumber
```  

Or you can specify a feature to run:
```bash
  $ cucumber features/market.feature
```  

Or tag (this can be any word that starts with @ sing placed before scenario), e.g.:
```bash
  $ cucumber -t @current
```

### Note

Testnet is being recreated from scratch before each scenario, so each scenario starts within a clean state.

The first run can take a little bit longer because it bootstraps the test net, next runs will much faster because it resets the state by restoring wallets from backup rather recreating everything from scratch.
  
If you want to pause scenarios execution and keep testnet running after scenario to inspect the nodes via http rpc, insert @pause tag before scenario.

In order to access the nodes via web wallet you need to create htdocs symlink to web_wallet/generated or to web_wallet/build, e.g. 

  $ ln -s ../web_wallet/generated htdocs
  
And open http://localhost:5690 (or 5691/5692) in your browser.



### Troubleshooting

All rpc calls are dumped to features.log, so if something went wrong examine features.log - this may give you some idea.

Also you can always start from scratch by removing ./tmp dir
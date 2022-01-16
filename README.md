## Joader

Joader is hign performance loader for training multiple DNN jobs.

## Build with
install [Python3.8](https://www.python.org/downloads/release/python-380/)

install python requirements:
```sh
cd frontend
pip install -r requirements.txt
```

install [rust](https://www.rust-lang.org/tools/install)

install [opencv](https://opencv.org/) and [opencv-rust](https://github.com/twistedfall/opencv-rust)


rust build:
```sh
cd backend
cargo build
```

## Usage
### singleton
start backend
```
cd backend
cargo run
```
backend args:
```
cd backend
cargo build --release
./target/release/joader --help
```

Add frontend to the system path of python

frontend example of dummy
``` py
from dataset.dataset import Dataset, DatasetType
from loader.loader import Loader
import grpc

channel = grpc.insecure_channel('0.0.0.0:4321')
name = "DummyDataset"
len = 1000
ds = Dataset(name=name, location="", ty=DatasetType.DUMMY)
for i in range(0, len):
    ds.add_item([str(i)])
ds.create(channel)
loader = Loader.new(dataset_name=name,
                    name="dummy_loader", ip='0.0.0.0:4321', nums=1)
for i in range(len):
    res = loader.next()
loader.delete()
ds.delete(channel)
```

## Roadmap

- [x] Add dataset
- [x] Add loader
- [x] Add Sampler
- [x] Add thread-pool for backend
- [x] Support LMDB
- [ ] Support Filesystem
- [ ] Support filtering
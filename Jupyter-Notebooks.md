It can be handy to use Jupyter (previously IPython) notebooks in combinations with the Ocropy API (`ocrolib` module).

We assume that you already have successfully installed ocropus. Then you just need Jupyter with Python 2 support:

```
pip install --upgrade pip
sudo pip install jupyter
```

To start Jupyter just type
```
jupyter notebook
```
which will open a new jupyter notebook in your browser.

To use the `ocrolib` inside a Jupyter notebook just add the line
```
import ocrolib
```
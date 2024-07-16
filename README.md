# hello world with fastapi
1. 'poetry new fastapi_helloworld_online'
2. 'cd fastapi_helloworld_online'
3. Select your project with VScode
4. open file 'pyproject.toml'
'''
[tool.poetry]
name = "fastapi-helloworld-online"
version = "0.1.0"
description = ""
authors = ["syednaveedkhalid <syednaveedkhalid6489@gmail.com>"]
readme = "README.md"

[tool.poetry.dependencies]
python = "^3.12"


[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
'''

5. install new packages in poetry project
   'poetry add fastapi "uvicorn[standard]"'
   '''
[tool.poetry.dependencies]
python = "^3.12"
fastapi = "^0.111.1"
uvicorn = {extras = ["standard"], version = "^0.30.1"}
'''

6. create 'main.py' location 'fastapi_helloworld_online\main.py'
'''
@app.get("/")
def index():
    return {"Hello": "World"}

@app.get("/piaic/")
def piaic():
    return{"organization": "piaic"}
'''

7. install packages 'pip install fastapi uvicorn'
8. run server
   'poetry run uvicorn fastapi_helloworld_online.main:app --reload'
9. 'http://127.0.0.1:8000/'
   * 'http://127.0.0.1:8000/piaic/'
10. 'http://127.0.0.1:8000/docs'
11. write your own test
   * 'test/test_main.py'
   '''
   from fastapi.testclient import TestClient
from fastapi_helloworld_online.main import app


def test_root_path():
    client = TestClient(app=app)
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"Hello": "World"}

def test_piaic_description():
    client = TestClient(app=app)
    response = client.get("/piaic/")
    assert response.status_code == 200
    assert response.json() == {"organization": "piaic"}

def test_third_check():
    client = TestClient(app=app)
    response = client.get("/piaic/")
    assert response.status_code == 200
    assert response.json() == {"organization": "ABC"}
   '''

12. 'poetry run test -v'
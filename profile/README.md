
# VKU.NewEnergy
[TEST HERE](http://www.vku-newenergy.tech/)
# AI-powered Vietnamese Laws Searching System
This project is aimed to build a searching system for Vietnamese Laws that utilized AI powers.
It includes three repositories. They are code for [User Interface](https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-fe), [Backend Services](https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-searching-service), and [AI System](https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-ai).
> **Note** : You can find information about third-party licenses which used in this project in [this file](https://github.com/VKU-NewEnergy/.github/blob/main/profile/THIRD_PARTY_LICENSE_README.txt).
📦 Dataset
- [Codification](https://phapdien.moj.gov.vn/Pages/home.aspx)
- [Vietnamese legal documents](https://vbpl.vn/pages/portal.aspx)
## I. Getting Started
### Clone repos
```
mkdir vku-newenergy
cd vku-newenergy
git clone https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-fe.git
git clone https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-searching-service.git
git clone https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-ai.git
```
## II. Requirements
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [GNU Make](https://www.gnu.org/software/make/)
- [PostgreSQL CLI](https://www.postgresql.org/download/)
- [NodeJS 20 or higher](https://nodejs.org)
- [Yarn 1.22 or higher](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable)
- [Python v3.10.10](https://www.python.org/downloads/release/python-31010/)
- [gdown](https://github.com/wkentaro/gdown)
- [Unzip CLI](https://www.tecmint.com/install-zip-and-unzip-in-linux/)
## III. Setting up
### Front-end
> ⚠️ Always cd into project root before doing anything
```
cd vietnamese-laws-ai-system-fe
```

#### 1. Prerequisites
```bash
# clone the repo
git clone https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-fe

# cd to the repo
cd vietnamese-laws-ai-system-fe

# make a copy of .env.example as .env and change the values accordingly
cp .env.example .env
```

#### 2. Launch app by `make` command
```bash
make install
```

#### 3. Development
#### 3.1 Install dependencies
```
yarn install
```
#### 3.2 Run the development server
```
yarn dev
```
#### 4. Production
#### 4.1 Build container
```
docker build -t vietnam-laws-fe .
```
#### 4.2 Run container
```
docker run -p 3000:3000 vietnam-laws-fe
```
### Backend services
> ⚠️ Always cd into project root before doing anything
```
cd vietnamese-laws-ai-system-searching-service
```

#### 1. Launch app by `make` command
```
make install
```
#### 2. Launch app manually
#### 2.1. Prepare environment
```sh
make prepare-environments
```
#### 2.2. Start services
```sh
docker compose up -d --build
```
#### 3. Prepare data for database
- Download database import file from this [link](https://drive.google.com/file/d/1oFczUDpweAyh3tivdDH3t38L5FSPAZht/view)
- Create `init-data` directory in root directory.
- Extract and copy all files to `init-data` directory.
#### 4. Import data into database
```sh
make import-data
```
### AI System
> ⚠️ Always cd into project root before doing anything
```
cd vietnamese-laws-ai-system-ai
```

### Training data
- [Google Drive](https://drive.google.com/file/d/1GXDA94yYdC-dSASfCED9Q06-BVbHYSAe/view?usp=sharing)

#### 1. Prepare environment
- Create `.env` file in the root directory.
- Copy content from `.env.example` and change to your correct data.
#### 2. Start app
#### 2.1 Using `make` command
```bash
make install
```
#### 2.2 Run locally
```
pip install -r requirements.txt
python main.py
```
#### 2.3 Using docker
```
docker compose up
```
Afterwards, FastAPI automatically generates documentation based on the specification of the endpoints you have written. You can find the docs at http://localhost:9000/docs.
## IV. API List
#### 1. Topics API
- Get all topics: [GET]: `/api/v1/topics`
#### 2. Subjects API
- Get all subjects: [GET]: `/api/v1/subjects`

| Params      | Description   | Default     |
| ----------- | -----------   | ----------- |
| topic_id    | Topic ID      | null        |

#### 3. Indexing API
- Get all indexing: [GET]: `/api/v1/indexing`

| Params      | Description   | Default     |
| ----------- | -----------   | ----------- |
| subject_id  | Subject ID    | null        |

#### 4. Charters API
- Get all indexing: [GET]: `/api/v1/charters`

| Params      | Description                         | Default     |
| ----------- | -----------                         | ----------- |
| page        | Page number                         | 1           |
| size        | Size of each page                   | 50          |
| q           | Search text by title or description | ''          |

#### 5. Legal Documents API
- Get all indexing: [GET]: `/api/v1/legal-documents`

| Params      | Description   | Default     |
| ----------- | -----------   | ----------- |
| subject_id  | Subject ID    | null        |

#### 6. Feedback API
- Submit a feedback for searching charter: [POST] `/api/v1/feedback`

| Body      | Description   | Required     |
| ----------- | -----------   | ----------- |
| charter_title  | Title of charter    | true        |
| search_keyword  | Keyword when searching    | true        |
| user_email  | Email of submitter    | false        |
| response  | Content of feedback    | false        |
| rate  | Satisfaction of submitter (0 - 5)    | true        |

#### 7. Glossaries API

- Get all indexing: [GET]: `/api/v1/glossaries`

| Params | Description                         | Default |
| ------ | ----------------------------------- | ------- |
| page   | Page number                         | 1       |
| size   | Size of each page                   | 50      |
| q      | Search text by term or description | ''      |

## V. Database Design
![image](https://github.com/VKU-NewEnergy/.github/assets/69782094/a6bde3a3-5405-4440-9820-d6c89b3039f8)
## VI. Application System Architecture
![image](https://github.com/VKU-NewEnergy/.github/assets/69782094/1daa2464-f6ce-4b45-ae1f-d6995be0fe31)
## VI. Retrieval QnA System Architecture
![image](https://github.com/VKU-NewEnergy/.github/assets/69782094/9f531af8-ec5d-4a98-a714-fd35db55882a)
![image](https://github.com/VKU-NewEnergy/.github/assets/69782094/bbcd9160-2423-4dd9-9dad-12862293d660)
--------------------------------------------------------------------------------------------------------
📝 License
This project is licensed under the terms of the [Apache V2.0](https://github.com/VKU-NewEnergy/.github/blob/main/profile/LICENSE) license.

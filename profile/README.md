# VKU.NewEnergy
# AI-powered Vietnamese Laws Searching System
This project is aimed to build a searching system for Vietnamese Laws that utilized AI powers.
It includes three repositories. They are code for [User Interface](https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-fe), [Backend Services](https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-searching-service), and [AI System](https://github.com/VKU-NewEnergy/vietnamese-laws-ai-system-ai).
> **Note** : You can find information about third-party licenses which used in this project in [this file](https://github.com/VKU-NewEnergy/.github/blob/main/profile/THIRD_PARTY_LICENSE_README.txt).
# I. Getting Started
## Clone repos
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
- [NodeJS v20](https://nodejs.org)
- [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable)
- [Python v3.10.10](https://www.python.org/downloads/release/python-31010/)
## III. Setting up
### Front-end
> ⚠️ Always cd into project root before doing anything
> cd vietnamese-laws-ai-system-fe
#### 1. Development
Install dependencies
```
yarn install
```
Run the development server
```
yarn dev
```
#### 2. Production
Build container
```
docker build -t vietnam-laws-fe .
```
Run container
```
docker run -p 3000:3000 vietnam-laws-fe
```
### Backend services
> ⚠️ Always cd into project root before doing anything
> cd vietnamese-laws-ai-system-searching-service
#### 1. Prepare environment
- Copy environment file
```sh
make prepare-environments
```
#### 2. Start services
```sh
docker compose up -d --build
```

#### 3. Prepare data for database
- Download database import file from this [link](https://drive.google.com/file/d/1AT11PWQ_1Jsds-RiMM55fqgT_ynnKsbw/view)
- Create `init-data` directory in root directory.
- Extract and copy all files to `init-data` directory.
#### 4. Import data into database
```sh
make import-data
```
### AI System
> ⚠️ Always cd into project root before doing anything
> cd vietnamese-laws-ai-system-ai
#### 1. Prepare environment
- Create `.env` file in the root directory.
- Copy content from `.env.example` and change to your correct data.
#### 2. Start app
#### 2.1 Run locally
```
pip install -r requirements.txt
python main.py
```
### 2.2 Using docker
```
docker compose up
```
Afterwards, FastAPI automatically generates documentation based on the specification of the endpoints you have written. You can find the docs at http://localhost:9000/docs.
## IV. API List
### 1. Topics API
- Get all topics: [GET]: `/api/v1/topics`
### 2. Subjects API
- Get all subjects: [GET]: `/api/v1/subjects`

| Params      | Description   | Default     |
| ----------- | -----------   | ----------- |
| topic_id    | Topic ID      | null        |

### 3. Indexing API
- Get all indexing: [GET]: `/api/v1/indexing`

| Params      | Description   | Default     |
| ----------- | -----------   | ----------- |
| subject_id  | Subject ID    | null        |

### 4. Charters API
- Get all indexing: [GET]: `/api/v1/charters`

| Params      | Description                         | Default     |
| ----------- | -----------                         | ----------- |
| page        | Page number                         | 1           |
| size        | Size of each page                   | 50          |
| q           | Search text by title or description | ''          |

### 5. Legal Documents API
- Get all indexing: [GET]: `/api/v1/legal-documents`

| Params      | Description   | Default     |
| ----------- | -----------   | ----------- |
| subject_id  | Subject ID    | null        |

### 6. Feedback API
- Submit a feedback for searching charter: [POST] `/api/v1/feedback`

| Body      | Description   | Required     |
| ----------- | -----------   | ----------- |
| charter_title  | Title of charter    | true        |
| search_keyword  | Keyword when searching    | true        |
| user_email  | Email of submitter    | false        |
| response  | Content of feedback    | false        |
| rate  | Satisfaction of submitter (0 - 5)    | true        |

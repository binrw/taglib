pipeline {
    agent any

    stages {
        stage('Checkout repo') {
            steps {
                git 'https://github.com/binrw/taglib'
            }
        }
        stage('Check dependencies') {
            steps {
                //Todo
                echo 'Dependencies: utf8cpp, zlib, cppunit'
            }
        }
        stage('Compile taglib') {
            steps {
                //Todo
                sh 'rm -rf build && mkdir build'
                sh 'cmake -B build -DBUILD_SHARED_LIBS=ON -DVISIBILITY_HIDDEN=ON -DBUILD_TESTING=ON -DBUILD_EXAMPLES=ON -DBUILD_BINDINGS=ON -DCMAKE_BUILD_TYPE=Release'
                sh 'cmake --build build --config Release'
            }
        }
        stage('Run taglib Tests') {
            steps {
                sh 'cmake --build build --config Release --target check'
            }
        }
        stage('Build taglib binaries') {
            steps {
                sh 'rm -rf build-outputs && cmake --install build --config Release --prefix build-outputs --strip'
            }
        }
        stage('Deploy taglib') {
            steps {
                sh 'cd /Users/robert/Desktop/example_nfs_share/ && mkdir -p taglib/latest'
                sh 'cd /Users/robert/Desktop/example_nfs_share/ && rm -rf taglib/previous'
                
                sh 'cd /Users/robert/Desktop/example_nfs_share/ && mv taglib/latest taglib/previous'
                sh 'rsync -avP --delete build-outputs/* /Users/robert/Desktop/example_nfs_share/taglib/latest/'
                
            }
        }

    }
}

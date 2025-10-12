pipeline{
	agent any
	stages{
		stage("Pull Code from Github repo"){
			steps{
				echo "pulling code from GitHub ......"
			}
		}
		stage("Build"){
			steps{
				echo "Building Packaged from Code ......"
			}
		}
		stage("Test"){
			steps{
				echo "Testing Package ......"
			}
		}
		stage("Deploy"){
			steps{
				echo "Deploying Application ......"
			}
		}
	}
}

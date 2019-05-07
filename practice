<?php
	class student extends ObjectModel
	{
		public $id;
		public $name;
		public $birthdate;
		public $status;
		public $avg;

		public static $definition = array(
		  'table' => 'students',
		  'primary' => 'id_group',
		  'multilang' => true,
		  'fields' => array(
			'studentId'  => array('type' => self::TYPE_INT, 'validate' => 'isUnsignedInt'),
			'name'       => array('type' => self::TYPE_STRING),
			'birthdate'  => array('type' => self::TYPE_DATE),
			'status'	 => array('type' => self::TYPE_BOOL),
			'avg'		 => array('type' => self::TYPE_DOUBLE)
		  ),
		);
		
		public function __construct($newId, $newName, $newBirthdate, $newStatus, $newAvg){
			$this->id = $newId;
			$this->name = $newName;
			$this->birthdate = $newBirthdate;
			$this->status = $newStatus;
			$this->avg = $newAvg;
		}
		
		public function getAllStudents(){
			$sql = new DbQuery();
			$students = array();
			$studentsList = array();
			$sql->select('*');
			$sql->from(_DB_PREFIX_.'students', 's');
			$sql->where('s.id_group = 1');
			$students = Db::getInstance()->executeS($sql);
			if(!$students ||
				is_null($students)){
				return null;
			}
			foreach $students as $student{
				$newStudent = new student($student['studentId'], $student['name'], $student['birthdate'], $student['status'], $student['avg']);
				$studentsList[] = $newStudent;
			}
			return $studentsList;
		}
		
		public function getBestStudent(){
			$sql = 'SELECT s.`*`
			FROM `'._DB_PREFIX_.'students` s
			WHERE s.`avg` = 
			SELECT MAX(avg)
			FROM `'._DB_PREFIX_.'students`';
			$bestStudent = Db::getInstance()->executeS($sql);
			if(!$bestStudent ||
				is_null($bestStudent)){
				return null;
			}
			$newStudent = new student($bestStudent['studentId'], $bestStudent['name'], $bestStudent['birthdate'], $bestStudent['status'], $bestStudent['avg']);
			return $newStudent;
		}
		
		public function getMaxAvg(){
			$sql = 'SELECT MAX(s.avg)
			FROM `'._DB_PREFIX_.'students` s';
			$maxAvg = Db::getInstance()->executeS($sql);
			if(!$maxAvg ||
				is_null($maxAvg)){
				return null;
			}
			$newAvg = $maxAvg[0];
			return $newAvg;
		}		
	}
?>

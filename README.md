# newrepo

sample code

public function SMSLog($phone_number, $message, $location_id, $sms_type){
		$sms_log['phone_number'] = $this->logPhoneNumber;
		$sms_log['message'] = $message;
		$sms_log['location_id'] = (string)$location_id;
		$sms_log['sms_type'] = $sms_type;
		$sms_log['email'] = '';
		$sms_log['date'] = date('Y-m-d');				
		$sms_log['timestamp'] = (int) time();	
		$sms_log['total_credits'] = $this->total_credits;
		$sms_log['credits_per_sms'] = $this->credits_per_sms;
		if(empty($this->current_credits)){
			$sms_log['current_credits'] = $this->total_credits;
		} else{
			$sms_log['current_credits'] = $this->current_credits-$this->credits_per_sms;
		}
		//update current status in company table
		$updateCurrentCredits = Company::where('id',$this->company_id)->update(['current_credits' => $sms_logs['current_credits']]);
		$data = SmsLog::create($sms_log);	
	}

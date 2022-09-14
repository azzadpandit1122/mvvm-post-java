# mvvm-post-java

public class DashBoardViewModel extends AndroidViewModel {

    public UserRepository userRepository;

     
      private LiveData<List<CareerResponseModel>> careerExploreMutableLiveData = new MutableLiveData<>();

    
     public DashBoardViewModel(@NonNull Application application) {
        super(application);
        userRepository = new UserRepository();
    }
    
     public void getExploreCareer(Context context) {
        this.careerExploreMutableLiveData = userRepository.UserCareerExplore(new SaveData(context).getSessionCookie());

    }

    public LiveData<List<CareerResponseModel>> getUserExploreCareers() {
        return careerExploreMutableLiveData;
    }

}


//main actvity 
      //oncreate
      mCrrExpVwMdl = ViewModelProviders.of(getActivity()).get(SharedViewModel.class);
      getAllExploreCareer();
        mViewModel.getExploreCareer(getActivity());
        
        
         public void getAllExploreCareer() {
        mViewModel.getUserExploreCareers().observe(getViewLifecycleOwner(), Response -> {
            if (Response != null) {

                mCareerResponse = Response;
                mArrayList.addAll(mCareerResponse);
                new SaveData(getActivity()).setFilterDataCareer(mCareerResponse);

                adapter.notifyDataSetChanged();
            }
        });
    }


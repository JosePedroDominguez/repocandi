    public IRepository<CandidateIndustryEntity> CandidateIndustryRepository
    {
        get
        {
            if (_candidateIndustryRepository == null)
                _candidateIndustryRepository = new Repository<CandidateIndustryEntity>(_context);

            return _candidateIndustryRepository;
        }
    }

    public IRepository<CandidateStateHistoryEntity> CandidateStateHistoryRepository
    {
        get
        {
            if (_candidateStateHistoryRepository == null)
                _candidateStateHistoryRepository = new Repository<CandidateStateHistoryEntity>(_context);

            return _candidateStateHistoryRepository;
        }
    }

    public IRepository<TypeStateEntity> TypeStateRepository
    {
        get
        {
            if (_typeStateRepository == null)
                _typeStateRepository = new Repository<TypeStateEntity>(_context);

            return _typeStateRepository;
        }
    }

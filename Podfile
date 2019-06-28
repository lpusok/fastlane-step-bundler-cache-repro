# frozen_string_literal: true

# =================== #
#   Podspec Sources   #
# =================== #

source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/SpotHero/Podspecs.git'

# ========================= #
#   Target Configurations   #
# ========================= #

# Inhibits all the warnings from the CocoaPods libraries.
inhibit_all_warnings!

# Use frameworks instead of static libraries for Pods.
use_frameworks!

# Specifies the Xcode workspace at the root
workspace 'SpotHero.xcworkspace'

# ============= #
#   Constants   #
# ============= #

# The version number shared by all Facebook pods
FACEBOOK_VERSION = '~> 4.39'

# Our minimum supported version of iOS
IOS_MINIMUM_VERSION = '11.0'

# Our minimum supported version of watchOS
WATCHOS_MINIMUM_VERSION = '3.0'

# ======================= #
#   Convenience Methods   #
# ======================= #

# =================== #
#   Pod Definitions   #
# =================== #

# Pods used by all targets
def shared_pods
  # Swap for local development in the same path, but remember to swap back and
  # run pod update SpotHeroSwiftAPI again to not hit other pods!
  # pod 'SpotHeroSwiftAPI', :path => '../SpotHeroSwiftAPI'
  pod 'SpotHeroSwiftAPI', '~> 6.1.0'

  pod 'SAMKeychain', '~> 1.5.3'

  # Using our own fork since Vokoder is no longer maintained
  pod 'Vokoder/Swift', git: 'https://github.com/spothero/Vokoder.git', branch: 'master'
end

# Pods used by Core and iOS targets
def shared_ios_pods
  pod 'Analytics', '~> 3.6.10' # this is Segment
  pod 'Crashlytics', '~> 3.12.0' # includes Fabric dependency
  pod 'DTCoreText', '~> 1.6.21' # Obj-C, last released Aug 2017
  pod 'MBProgressHUD', '0.9.2' # don't update without checking how bad it breaks shit
  pod 'SDWebImage', '~> 4.4.3'
  pod 'Sentry', '~> 4.3.4'
  pod 'SpotHero_iOS_Google_Places_Wrapper', '~> 1.2.0'
  pod 'Stripe', '~> 14.0.0'
  pod 'TTTAttributedLabel', '~> 2.0.0' # Obj-C, last released May 2016

  # Using our own fork since Vokoder is no longer maintained
  pod 'Vokoder/DataSources',  git: 'https://github.com/spothero/Vokoder.git', branch: 'master'
  pod 'ZXingObjC', '~> 3.2.2' # Obj-C, to be deprecated in favor of BarcodeHero
end

# Pods used by iOS app only
def ios_app_pods
  # SpotHero Pods or Forks
  pod 'SHEmailValidator'
  pod 'ParkonectSDK', '~> 0.2.0'

  # Third Party Pods
  pod 'AppsFlyerFramework', '~> 4.8.11'
  pod 'Branch', '~> 0.25.10'
  pod 'CardIO', '~> 5.4.1'
  pod 'FBSDKCoreKit', FACEBOOK_VERSION
  pod 'FBSDKLoginKit', FACEBOOK_VERSION
  pod 'Firebase', '~> 5.20.2', subspecs: ['Analytics', 'Core']
  pod 'FlashAccess', path: 'SpotHero/vendors/FlashAccess/FlashAccess.podspec'
  pod 'GoogleSignIn', '~> 4.4.0'
  pod 'OptimizelySDKiOS', '~> 3.0.2'
  pod 'SwiftyGif', '~> 4.2.0'
  pod 'SwiftLint', '~> 0.32.0'

  # Using our own fork so that we only use the Appboy Core dependency, otherwise Segment-Appboy defaults to using all their UI dependencies
  # If reverting back to using Appboy (including their UI framework) ensure you update our import of SDWebImage to include the /GIF subspec
  # and that it matches the version Appboy needs: https://github.com/Appboy/appboy-ios-sdk/blob/master/Appboy-iOS-SDK.podspec
  pod 'Segment-Appboy', git: 'https://github.com/spothero/appboy-segment-ios.git', branch: 'master'

  # Official podspec doesnt exist and local podspec is outdated, using the latest commit
  pod 'GenericPasswordExtension',
      git: 'https://github.com/joelastpass/generic-password-app-extension',
      commit: '4f9a65df3b5131178f380245cdcc5ec980c659a7'
end

# Pods used by all test targets
def shared_testing_pods
  pod 'VOKMockUrlProtocol', '~> 2.4.0'
end

# Pods used by UI test targets
def ui_testing_pods
  pod 'KIF', '~> 3.7.4'
end

# =============== #
#   All Targets   #
# =============== #

# The global Podfile has an implicit abstract_target
# All pods listed here will be shared across all targets

shared_pods

# =============== #
#   iOS Targets   #
# =============== #

abstract_target 'SpotHero-iOS' do
  project 'SpotHero/SpotHero.xcodeproj'

  platform :ios, IOS_MINIMUM_VERSION

  shared_ios_pods

  target 'SpotHero' do
    ios_app_pods

    target 'SpotHeroTests' do
      inherit! :search_paths

      shared_testing_pods
    end

    target 'SpotHeroUITests' do
      inherit! :search_paths

      shared_testing_pods
      ui_testing_pods
    end
  end

  target 'SpotHeroiMessage'
  target 'TodayExtensionWidget'
end

# =================== #
#   watchOS Targets   #
# =================== #

abstract_target 'SpotHero-watchOS' do
  project 'SpotHero/SpotHero.xcodeproj'

  platform :watchos, WATCHOS_MINIMUM_VERSION

  target 'SpotHeroWatchExtension'
end

# ================ #
#   Core Targets   #
# ================ #

abstract_target 'SpotHeroCore' do
  project 'SpotHeroCore/SpotHeroCore.xcodeproj'

  target 'SpotHeroCore-iOS' do
    platform :ios, IOS_MINIMUM_VERSION

    shared_ios_pods

    target 'SpotHeroCoreDemo'
    target 'SpotHeroCoreTests'
  end

  target 'SpotHeroCore-watchOS' do
    platform :watchos, WATCHOS_MINIMUM_VERSION
  end
end

# ================================================ #
#   Generated Acknowledgement File Customization   #
# ================================================ #

# Responsible for the generated acknowledgements.markdown file
class ::Pod::Generator::Acknowledgements
  def header_title
    "© SpotHero #{Date.today.year}. All Rights Reserved"
  end

  def header_text
    "\nPortions of this application may utilize the following copyrighted material, the use of which is hereby acknowledged"
  end

  def footnote_text
    ''
  end
end

# ======================== #
#   Post Install Scripts   #
# ======================== #

post_install do |installer|
  require 'fileutils'

  # copy the autogenerated acknowledgements file into the project
  FileUtils.cp_r(
    'Pods/Target Support Files/Pods-SpotHero-iOS-SpotHero/Pods-SpotHero-iOS-SpotHero-acknowledgements.markdown',
    'SpotHero/SpotHero/Assets/attribution_notices.md',
  )

  # make ZXingObjC work inside extensions
  zxing_targets = installer.pods_project.targets.select { |target| target.name =~ /ZXingObjC/ }
  zxing_targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['APPLICATION_EXTENSION_API_ONLY'] = 'YES'
    end
  end

  # make DTCoreText work in iMessage
  dt_core_text_targets = installer.pods_project.targets.select { |target| target.name =~ /DTCoreText/ }
  dt_core_text_targets.each do |target|
    target.build_configurations.each do |config|
      # disable this next line to fix warnings
      # config.build_settings['CONFIGURATION_BUILD_DIR'] = '$PODS_CONFIGURATION_BUILD_DIR'
      config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= ['$(inherited)', 'DT_APP_EXTENSIONS=1']
    end
  end

  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      # Disable Code Coverage for Pods projects
      # Thanks, Uncle Aijaz! http://aijazansari.com/2016/12/25/code-coverage/index.html
      config.build_settings['CLANG_ENABLE_CODE_COVERAGE'] = 'NO'

      ## Set watchOS pod's WATCHOS_DEPLOYMENT_TARGET to 3.0 to fix Xcode10 app store minimum deployment target issue
      config.build_settings['WATCHOS_DEPLOYMENT_TARGET'] = WATCHOS_MINIMUM_VERSION if config.build_settings['SDKROOT'] == 'watchos'
    end
  end
end
